Developer Information
=====================

Modification Guidelines
***********************
#. **Never modify code files**: When extending or modifying pointshop 2 the first guideline is to never modify any of the core files. You can use hooks and global functions to extend the script or modify functionality. This makes sure that there are as little conflicts between addons as possible. If you need a specific hook or if modification of core files is a much easier solution to a general problem, please get in touch.

#. **Skin your panels only in derma skins**: To make sure that skins can provide a consistent experience, it is important that Paint functions are never directly overwritten. Instead use Derma_Hook and extend the base skin. This gives skin creator the chance to support your addon without messy hooks and overwrites.

#. **Avoid global variables**: Use local variables or create a single global table for your addon to store globals. This avoids cluttering the global namespace, is faster and avoids conflicts.

#. **Avoid direct database queries**: Pointshop 2 makes heavy use of LibK as a database abstraction layer. This enables easy swapping of the databases and makes it possible to avoid many security issues. While you are not required to use LibK models you are encouraged to do so as it automates table creation and removal and allows you to hook into the export, import and backup mechanisms of Pointshop 2 without additional work.

Getting Started
***************
To get started with Pointshop 2 development, first read the information on module creation.
Modules are the main way to modify and extend Pointshop 2. They provide many automated facilities 
that make it very easy to extend the script.

After that a good way to start is to check out the examples.

.. _dev-options:

Developer Options
-----------------
To make development and debugging of the script easier there are a few options for developers. If you experience any errors please also turn these settings on as it will help track errors down.

Within *addons/libk/lua/libk/shared/2_sh_libk.lua* LibK developer settings can be configured.

Defaults
********

   LibK.Debug = false
   
   LibK.LogLevel = 2 --Requires Debug
   
   LibK.LogSQL = false
  
Developer
*********

   LibK.Debug = true
   
   LibK.LogLevel = 4 --Requires Debug
   
   LibK.LogSQL = true

``LibK.LogSQL`` logs every query that is generated and sent to the database. This can slow down the server significantly and creates large log files. Only use it if needed.

The reload command
******************

For easier development the ``pointshop2_reload`` command to fully reload the script was added. It requires LibK to be in debug mode as well as the user to be an administrator. The command will reload every part of the script, including the database. You can use this to quickly test changes without having to change the map. The command only works for existing files, when adding new files you have to do a map change. 

.. note::
   The ``pointshop2_reload`` command is currently broken on linux as file changes are not properly picked up by the game.

Examples
********

- Full tutorial to create an item: https://physgun.netlify.app/pointshop-2/custom-item-part1/
- Bodygroups Chooser by AlphaWolf: https://github.com/snowywolf/Pointshop-2-Bodygroups
- Blur Skin by AlphaWolf: https://github.com/snowywolf/Pointshop-2-Skin
- Full tutorial on how to create a low gravity item: `Tutorial <https://www.physgun.com/pointshop-2/custom-item-part1/>`_ `Code <https://github.com/Kamshak/ps2-lowgravity>`_
