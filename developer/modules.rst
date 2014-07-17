Module Creation
---------------

Modules are the best way to extend pointshop. Through them new item creators can 
be added.

Structure
=========
The module structure is very simple. Each module is a folder within the *lua/ps2/modules* folder.
Every file in this folder is recursively loaded by the module loader. The realm is determined by
the file prefix (sh, cl, sv). Client files are automatically AddCSLuaFile'd. 


Within this folder the module description file *sh_module.lua* needs to be placed.
Here you set up the module table (:lua:class:`MODULE`) which contains information such as the author and name of the module, then register it using :lua:func:`Poinsthop2.RegisterModule(MODULE)`.

Adding custom Item Types
========================

.. note::
    
    Creating custom item types is an advanced topic and requires an understanding of object oriented patterns. It is recommended to look at the items included in the script as an example when reading this section. Good candidates are the Trail and Playermodel items, which show very simple items. A complex example is provided with the Accessory/Hat, which uses multiple data models and a complex item creator.

Users should be able to create and modify items through the ingame gui. 

To understand the way items are created in Pointshop2 it is important to know that each item is handled on it's own and is unique. This means that even if the user owns ten items of the same type each is saved and handled individually. Technically, each item is an instance of a item class. Thus each "item" that is displayed for purchase at a shop is actually an *item class*. Instances of this class are the items which can be found in a player's inventory.

Internally this is achieved using the following components:

- **Persistence**: The persistence is the data model that is used to save all user defined properties (for example the model for a playermodel item, but also the item name and description). On server start the persistence is read and classes are dynamically generated. 

- **Item Base**: The item base defines the functionality of an item. This is defined in a lua file within **lua/kinv/items/pointshop**. Item bases can use mixins and extend existing bases. All item bases should extend ``base_pointshop_item``.

- **Item Creator**: This is the derma control which is used to create or modify an item. It inherits from ``DPointshopItemCreator``.


.. note::
    Unlike in pointshop 1, in pointshop 2 an item is an instance of an item class. A shop item is the representation of that class.


A **blueprint** is defined as the persistence, item base and creator for an item type.

Creating a persistence
======================

The first step when creating a custom item type is to create it's persistence. A persistence needs to be a LibK model, which is done by including the ``DatabaseModel`` mixin. 

Creating the data model
***********************

You can use this template:

.. highlight:: lua
.. code-block:: lua

    Pointshop2.ExamplePersistence = class( "Pointshop2.ExamplePersistence" )
    local ExamplePersistence = Pointshop2.ExamplePersistence
    
    ExamplePersistence.static.DB = "Pointshop2" --Use the database configured for Pointshop2
    
    
    ExamplePersistence.static.model = {
    	tableName = "ps2_examplepersistence", --needs to be unique
    	fields = {
    	    --holds the reference to the basic information (description, name, price)
    		itemPersistenceId = "int", 
    	    
    	    --Define your custom fields here
    		property1 = "string"
    	},
    	belongsTo = {
    	    -- Makes LibK automatically join the basic information table each times
    	    -- it is received from the database
    		ItemPersistence = {
    			class = "Pointshop2.ItemPersistence",
    			foreignKey = "itemPersistenceId"
    		}
    	}
    }
    
    ExamplePersistence:include( DatabaseModel ) --include the DatabaseModel mixin


It is important to specify the ``DB`` property to ``Pointshop2``. This makes the model save to the database as configured for Pointshop2. 

The model can be customized to contain as many fields as you need. If you need to save tables or nested data, consider joining another model (and creating a new belongsTo relationship) or simply use a field type that is serialized (json or luadata).

After doing this, a table will automatically be created and the model can now be used with LibK, which means that no queries have to be written to save or update items.

Implementing saving and updating logic
**************************************

.. note::

    LibK makes heavy use of *promises*. Using promises is required when saving or modifying models. They allow easy handling of asynchronous processes wihtout the need of messy nested callback chains. The promises script used (by Lexic) follows the javascript promises specification and the jQuery interface. More information: `General introduction <http://blog.parse.com/2013/01/29/whats-so-great-about-javascript-promises/>`_, `The jQuery interface documentation <http://api.jquery.com/jQuery.Deferred/>`_


When a pointshop item is created using an Item Creator, the persistence is passed a "save table". This table's structure is defined entirely by your creator. Usually it simply contains the model fields. The same function is called for updating items once they are modified. For this the static function ``createOrUpdateFromSaveTable`` has to be added. It creates (or on update retrieves) an instance of the own and any required models and then saves it to the database. All fields that the user can configure when creating a custom item need to be included into the model.

Create a new file within your module called **sh_model_<itemname>persistence.lua**.

For simple items you can follow this template:

.. highlight:: lua
.. code-block:: lua
    
    function ExamplePersistence.static.createOrUpdateFromSaveTable( saveTable, doUpdate )
        -- Firstly, save or update the basic item information.
    	local promise = Pointshop2.ItemPersistence.createOrUpdateFromSaveTable( saveTable, doUpdate )
    	:Then( function( itemPersistence )
    	    // First we fetch or create our persistence instance
    		if doUpdate then
    		    --We need to update an existing item.
    		    --Find the instance by using the itemPersistenceId and return it.
    			return ExamplePersistence.findByItemPersistenceId( itemPersistence.id )
    		else
    			local exampleInstance = ExamplePersistence:new( )
    			exampleInstance.itemPersistenceId = itemPersistence.id
    			return exampleInstance
    		end
    	end )
    	:Then( function( exampleInstance )
    	    // Then we update all fields
    		exampleInstance.property1 = saveTable.property1
    		
    		// And save changes to the database
    		return exampleInstance:save( )
    	end )
    	
    	return promise
    end

This concludes all of the serverside code that is needed for handling the creation and modification of items. 

Creating the item base
======================

The next step is to create the item base for your item type. To do this, create a new file within **lua/kinv/items/pointshop**. The name should be ``sh_base_<itemname>.lua`` you can also put your file into a subdirectory. Inside of the item base you can now overwrite any of the pointshop base functions and add item hooks as required.

.. todo::
    Item hook explanation

.. lua:function:: ITEM.static.generateFromPersistence(itemTable, persistenceItem)

    Decodes all information from the persistenceItem and adds fields and methods to the itemTable field.
    
    **itemTable**: A table containing the created class.
    **persistenceItem**: An instance of this item's persistence.
    

The next step is to make sure that the item persistence can be loaded into a valid instance of the item base. This is done by using the static ``generateFromPersistence`` method. This method is pretty much the opposite of the persistence's createOrUpdateFromSaveTable method (with the exception that a valid item class is created instead of a save table). To generate the item class first call the super class' method by invoking ``ITEM.super.generateFromPersistence( itemTable, persistenceItem.ItemPersistence )``. Next simple copy your item's properties over to the item class. You should set these to to the ``itemTable.static`` table since they belong to a class itself and not an instance (which would be an instantiated item in the player's inventory). 

Next you need to link the base to the persistence. To do this simply define a static ``getPersistence`` method which returns the persistence class used.

Example:


.. highlight:: lua
.. code-block:: lua

    ITEM.PrintName = "Pointshop Example Base"
    ITEM.baseClass = "base_pointshop_item"
    
    function ITEM.static.getPersistence( )
    	return Pointshop2.ExamplePersistence
    end
    
    function ITEM:OnEquip( ply )
    
    end
    
    function ITEM:OnHolster( ply )
        --note that ply == self:GetOwner()
    end

    function ITEM.static.generateFromPersistence( itemTable, persistenceItem )
    	ITEM.super.generateFromPersistence( itemTable, persistenceItem.ItemPersistence )
    	itemTable.property1 = persistenceItem.property1
    end

Within the item base you can also specify your own, custom icon controls for both, the shop and the inventory.

Adding the clientside creator
=============================

The last step is to create a custom editor control, which is shown when clicking the create item button. This is very easy to do, simply create a new file inside your module, called ``D<youritem>Creator``. It should inherit from ``DPointshopItemCreator`` and overwrite the ``SaveItem(saveTable)`` and ``EditItem(persistence, itemClass)`` methods. The ``SaveItem`` method populates the save table passed as argument with the settings set in the item creator. The ``EditItem`` method poulates the editor with the settings stored in the persistence. For ease of access the relevant itemClass is also passed as data from the persistence might be accessible easier in there.

Example template:

.. highlight:: lua
.. code-block:: lua

    local PANEL = {}
    
    function PANEL:Init()
        self.textEntry = vgui.Create( "DTextEntry" )
        self:addFormItem( "Property 1", self.textEntry )
    end

    function PANEL:SaveItem( saveTable )
    	self.BaseClass.SaveItem( self, saveTable )
    	saveTable.property1 = self.textEntry:GetText( )
    end
    
    function PANEL:EditItem( persistence, itemClass )
    	self.BaseClass.EditItem( self, persistence.ItemPersistence, itemClass )
    	
    	self.textEntry:SetText( persistence.property1 )
    end
    vgui.Register( "DExampleCreator", PANEL, "DItemCreator" )

Putting it all together: The blueprint
======================================

The only thing left to do now is to link the item to the menu and register it with the modules. This is done within sh_module.lua. Simply define all of your components in a :lua:class:`Blueprint`. 

Example:

.. highlight:: lua
.. code-block:: lua

    MODULE.Blueprints = {
    {
        label = "Example Item",
        base = "base_example", --The name is deduced from the filename
        icon = "pointshop2/playermodel.png", --Icon
        creator = "DExampleCreator"
    },
    
Creating a slot for your item
=============================

Slots are created using the function :lua:func:`Pointshop2.AddEquipmentSlot`

Example:

.. highlight:: lua
.. code-block:: lua
    
    Pointshop2.AddEquipmentSlot( "Example", function( item )
    	--Check if the item is an example item
    	return instanceOf( Pointshop2.GetItemClassByName( "base_example" ), item )
    end )

Adding custom Settings
======================
.. todo::
    Docs for creating settigns
    

Adding custom Tabs
==================
.. todo::
    Docs for creating tabs
