Developer API Reference
=======================
Use this to look up classes or methods.

.. note::
    Not every class is documented here. Look at the source code for usage examples.
    This is intended to explain data structures that might not be obvious at first as well as documenting the public interface.

Modules
-------

.. lua:class:: Blueprint
    
    A blueprint defines all properties needed for a custom item.

    .. lua:attribute:label:
    
        The label shown within the Create Items section of the management tab
        
    .. lua:attribute:icon:
    
        The path of the icon that is shown on the Create Button within the management tab
        
    .. lua:attribute:base:
    
        The name of the :class:`ItemBase` that all classes that are created via this blueprint inherit from
        
    .. lua:attribute:creator:
    
        The name of the derma control that is used by players to create item classes.


.. lua:Class:: SettingsCategory
    
    A table representing a category that contains one or more settings.
    The category's path is indicated by it's key in the table. The ``info`` key is used to provide a readable name for the category to be used in the configurator component.
    It contains multiple Settings, the path is again provided by the key.
    
.. lua:Class::Setting

    A table defining a Setting's properties. 
    
    .. lua:attribute:: value
        
        The default value of this setting. The type of the setting is automatically deduced from the type of the value unless it is explicitly specified.
        
    .. lua:attribute:: type
    
        The type of this setting. If it is not specified, it will be automatically deduced from the type of the ``value`` field.
        Possible types are:
            - **option**: Generates a dropdown which a user can select from. The possible values are provided in the ``possibleValues`` field of the setting.
            - **number**: Generates a number wang that can be used to enter any number
            - **boolean**: Generates a checkbox
    
    .. lua:attribute:: tooltip
    
        A string containing the tooltip that is given when hovering the setting in the settings editor.
    

.. lua:class:: MODULE

    The module information table. Contains information such as a module's blueprints and settings. This is to be defined in the module's *sh_module.lua*

    .. lua:attribute:: Name 
    
        The name of the module.
    
    .. lua:attribute:: Author 
        
        The author of the module
        
    .. lua:attribute:: RestrictGamemodes 
        
        A table containing gamemodes that this module is restricted to. The module will only be loaded if the active gamemode is in the list.
        
    .. lua:attribute:: Blueprints 
        
        A table containing :lua:class:`Blueprint`s that players can use.
        
    .. lua:attribute:: Settings 
        
        A table containing the settings of the module. A seperate table for each realm exists.
        ``Settings.Server`` is only sent to admins when changing the settings, ``Settings.Shared`` is synced with all clients.
        Accessing Settings is done by calling :lua:func:`Pointshop2.GetSetting`.
        Each realm settings table defines Settings that can be accessed and configured easily and can contain multiple ``SettingsCategory``s.
        Settings registered this way are automatically saved the the database when changed.
        
    .. lua:attribute:: SettingsButton 
        
        A table containing information about the settings button that will show up in the management tab.
        The table has three elements:
        
        ``label``: The label of the button 
        ``icon``: The icon of the button
        ``control``: The derma control that is created when clicking the button

.. lua:function:: Poinsthop2.RegisterModule(MODULE)

   Registers a :lua:class:`MODULE` to be used with Pointshop 2. 
   
.. lua:function:: Poinsthop2.GetSetting(moduleName, path)

    Returns the value of a setting from the given module according to the path.
    The bath is seperated by ``.`` characters. 
    
    Example:
    
    .. code-block:: lua
    
        print(Pointshop2.GetSetting("TTTIntegration", "RoundWin.Innocent"))
        
.. lua:function:: Pointshop2.AddEquipmentSlot(name, itemValidFunction)

    Registers a new equipment slot.
    
    **Name**:label of the slot that is shown underneath the slot's panel in the inventory.
    **itemValidFunction**: A function that takes an item as an argument and returns whether or not it can be equipped in the slot.
    
.. lua:function:: Pointshop2:AddTab(label, controlName, shouldShow)

    Adds a new tab to the top navigation of the pointshop.
    
    - **label**: The label of the tab.
    - **controlName**: The derma control that is created as panel.
    - **shouldShow**: **optional** A function returning whether or not the player should be able to see this tab.

.. lua:function:: Pointshop2:AddManagementPanel(label, icon, controlName, shouldShow)

    Adds a new tab to the side navigation of the management panel.
    
    - **label**: The label of the tab
    - **icon**: The tab's icon
    - **controlName**: The derma control that is created as panel
    - **shouldShow**: **optional** A function returning whether or not the player should be able to see this tab
    
    Example:

    .. code-block:: lua
    
        derma.DefineControl( "DPointshopManagementTab_Settings", "", PANEL, "DPanel" )

        Pointshop2:AddManagementPanel( "Settings", "pointshop2/advanced.png", "DPointshopManagementTab_Settings", function( )
            return PermissionInterface.query( LocalPlayer(), "pointshop2 managemodules" )
        end )
        
.. lua:function:: Pointshop2:AddInventoryPanel(label, icon, controlName, shouldShow)

    Adds a new tab to the side navigation of the management panel.
    
    - **label**: The label of the tab
    - **icon**: The tab's icon
    - **controlName**: The derma control that is created as panel
    - **shouldShow**: **optional** A function returning whether or not the player should be able to see this tab
