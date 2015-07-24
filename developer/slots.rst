Addings slots to existing modules
---------------------------------

Sometimes you will want an extra accessory or other type of slot. Since it is not recommended to create slots directly within the files that define them, a way to create new slots is described here.

Using the customizing addon
===========================
It is recommended to extend Pointshop 2 using a seperate addon. Simply download this addon and extract it into your addons folder: `Download <https://storage.sbg-1.runabove.io/v1/AUTH_66fcef59d5fa44c39f33878dbaeb3904/ps2_static/pointshop2-customizing.zip>`_. Put your new slot code into ``pointshop2-customizing/lua/ps2/modules/pointshop2/sh_customslots.lua``. As an example a new accessory slot is added. 

Adding accessory slots
======================

To add an accessory slot, use the function :lua:func:`Pointshop2.AddHatSlot`. This requires the Accessory/Hat module to be fully loaded, which is why the function should be called inside of the hook ``PS2_ModulesLoaded``.

Example:

.. highlight:: lua
.. code-block:: lua
    
	-- Adds a new Accessory slot
	hook.Add( "PS2_ModulesLoaded", "AddCustomSlots", function( )
		Pointshop2.AddHatSlot( "Accessory 3" )
	end )
	
Adding other slot types
=======================
Other slot types usually do not have convenience functions like the Accessory type. It is still possible to add these slots by duplicating the code. The slot code is defined in the file ``sh_slots.lua`` which can be found in the module's main folder.

It is also possible to define entirely custom slot types (for example VIP slots, universal slots, etc.) using :lua:func:`Pointshop2.AddEquipmentSlot`
