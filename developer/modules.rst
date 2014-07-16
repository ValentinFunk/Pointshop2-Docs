Module Creation
---------------

Modules are the best way to extend pointshop. Through them new item creators can 
be added.

Structure
*********
The module structure is very simple. Each module is a folder within the *lua/ps2/modules* folder.
Every file in this folder is recursively loaded by the module loader. The realm is determined by
the file prefix (sh, cl, sv). Client files are automatically AddCSLuaFile'd. 


Within this folder the module description file *sh_module.lua* needs to be placed.
Here you set up the module table which contains information such as the author and name of the module, then register it using :lua:func:`Pointshop2.RegisterModule`.

.. lua:class:: MODULE

    .. lua:attribute:: Name 
    
        The name of the module.
    
    .. lua:attribute:: Author 
        
        The author of the module
        
    .. lua:attribute:: RestrictGamemodes 
        
        A table containing gamemodes that this module is restricted to. The module will only be loaded if the active gamemode is in the list.
        
    .. lua:attribute:: Blueprints 
        
        A table containing Blueprints that players can use.
        
    .. lua:attribute:: Settings 
        
        A table containing the settings of the module.
        
    .. lua:attribute:: SettingsButton 
        
        A table containing information about the settings button that will show up in the management tab. 

.. lua:function:: Poinsthop2.RegisterModule(MODULE)

   Registers a :lua:class:`MODULE` to be used with Pointshop 2. 