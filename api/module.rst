Modules
=======

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
        print(Pointshop2.GetSetting("TTTIntegration", "RoundWin.Innocent"))