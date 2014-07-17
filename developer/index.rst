Developer Information
=====================

Pointshop2 was designed with modification, customization and extension in mind.
Wether you are extending or modifying the script, please follow the guildelines explained here.


Terms, Agreement and General Guidelines 
---------------------------------------

Pointshop 2 is designed to be a quality script. To maintain this experience to the user
addons and modifications need to conform to a high technical quality standard. You are obliged to
follow and adhere to these terms, otherwise you are not permitted to modify, use or look into the source 
code of pointshop2.

Code Review Process
*******************
To enforce the quality requirements to Pointshop 2 addons, it is mandatory to have it reviewed by
the author of Pointshop2. Independent of the addon's size and function it is necessary to get approval 
prior to publishing the script. Pointshop 2 is designed to be extended and modified through external scripts,
which is why as a developer you will receive support working with the codebase.

The code review is **free for publicly released scripts** and is available at a **fee of 10$ for every commercial script** (this includes coderhire jobs and scripts). This fee is used to maintain and update the developer documentation, add new functions and APIs for you to use and to provide premium support and advice when writing plugins. It also serves as a guard to protect against "5 second scripts" and low quality, hacked together scripts. Please note that if you do not comply to this agreement, your script will not be approved.

During the code review the code will be checked for exploits, problems with the existing codebase and incompatibilities with existing and future addons.
You will receive a written summary of the review and proposed changes. After fixing these problems you will receive a green light to release the addon. 
Follow up code reviews and code reviews for updates are free.

Support and information during the creation of a script are free. If you have any problems or a question about the codebase or
require additional functionality do not hesitate to get in touch via steam, coderhire PM or email.

To summarize:
For free (public scripts) or a small fee (commercial scripts) you get:

- Personal support
- Code review and quality assurance
- Compatibility testing against all addons in the program
- Listed on the script's page and officiall endorsement by Pointshop 2
- Promotion through Pointshop 2 communication channels

Modification Guidelines
***********************
#. **Never modify code files**: When extending or modifying pointshop 2 the first guideline is to never modify any of the core files. You can use hooks and global functions to extend the script or modify functionality. This makes sure that there are as little conflicts between addons as possible. If you need a specific hook or if modification of core files is a much easier solution to a general problem, please get in touch.

#. **Skin your panels only in derma skins**: To make sure that skins can provide a consistent experience, it is important that Paint functions are never directly overwritten. Instead use Derma_Hook and extend the base skin. This gives skin creator the chance to support your addon without messy hooks and overwrites.

#. **Avoid global variables**: Use local variables or create a single global table for your addon to store globals. This avoids cluttering the global namespace, is faster and avoids conflicts.

#. **Avoid direct database queries**: Pointshop 2 makes heavy use of LibK as a database abstraction layer. This enables easy swapping of the databases and makes it possible to avoid many security issues. While you are not required to use LibK models you are encouraged to do so as it automates table creation and removal and allows you to hook into the export, import and backup mechanisms of Pointshop 2 without additional work.

#. **Use lowercase file and folder names**: To keep linux compatibility please use lowercase file and foldernames. 

Getting Started
***************
To get started with Pointshop 2 development, first read the information on module creation.
Modules are the main way to modify and extend Pointshop 2. They provide many automated facilities 
that make it very easy to extend the script.

After that a good way to start is to check out the examples.

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

.. todo::
    Add Examples
