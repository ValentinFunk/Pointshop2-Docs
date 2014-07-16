Getting Started
===============

Installation
------------
To install Pointshop2 simply extract the zip you downloaded into the addons folder.
This will give you two folders: *addons/pointshop2* and *addons/libk*.

Next install PAC3, the newest version can always be found `here <https://github.com/CapsAdmin/pac3/archive/master.zip>`_.
Download and extract the zip, too. This will give you *addons/pac3-master*.

Final structure when everything is installed:
- garrysmod
   - addons
      - libk
      - pac3
      - pointshop2

Configuration
-------------
Pointshop2 requires no initial configuration! Once it is installed you are ready to go!
Restart your server and press F3 to open the menu. If nothing happens, use the "pointshop2" console command.
You can find all settings under the "Management" tab.

FastDL
------
Unless players already have the files from other places, they will see errors or texture problems if there is no FastDL system. If you haven't already set this up, see `here <http://maurits.tv/data/garrysmod/wiki/wiki.garrysmod.com/index70e8.html>`_. Pointshop2 automatically uses resource.AddFiles to add all required files to the server downloads. To avoid errors, please  upload the following files to your fastdl server:

- addons/pointshop2/materials
- addons/libk/resource

Make sure to upload them into your fastdl's root folder, i.e. *addons/pointshop2/materials* to *fastdl/materials*, NOT *fastdl/addons/pointshop2/materials*.


Advanced Configuration
======================

There are a few options in Pointshop2 that can be used to integrate the script more tightly into your system.

MySQL Setup
-----------
By default SQLite (via sv.db) is used to store all player and pointshop data. If you have a MySQL server you can also use MySQL with the script. This has the advantage of being more efficient for large amounts of data, enabling you to share items across multiple servers and allowing you to display data on the web. 

Switching from SQLite to MySQL means that the pointshop is reset - the data is not transferred across. If you wish to keep your data you have to manually export it.

To enable MySQL please follow these steps:

#. **Install the gmsv_mysqloo module**: Download the module from `facepunch <http://facepunch.com/showthread.php?t=1357773>`_ and follow the installation instructions for your operating system at the bottom of the post.

#. **Enable MySQL within LibK**: LibK is used for all database operations of Pointshop2. To enable MySQL support go into the configuration file *addons/libk/lua/libk/server/sv_libk_config.lua*. Set ``LibK.SQL.UseMysql = true`` and update the remaining settings with your database connection details. If you are hosting the database on a different machine than the gamemserver, make sure to allow external connections to the database. 

#. **Test the configuration**: After a server restart Pointshop2 will now connect to MySQL. If there are any errors when connecting to the database they will be shown in the server console and logged to garrysmod/data/LibK_Error.txt serverside.