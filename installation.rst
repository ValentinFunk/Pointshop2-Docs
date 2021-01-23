Getting Started
===============

Installation
------------
To install Pointshop2 simply extract the zip you downloaded into the addons folder.
This will give you two folders: *addons/pointshop2* and *addons/libk*.

Next install PAC3, the newest version can always be found `here <https://github.com/CapsAdmin/pac3/archive/master.zip>`_.
Download and extract the zip, too. This will give you *addons/pac3-master*.

You also need to add Pointshop 2 content to your server's workshop collection (see below).

Final structure when everything is installed:

- garrysmod
   - addons
      - libk
      - pac3
      - pointshop2
      
Installing Workshop Content to the Server
-----------------------------------------

You need to add the `Content Addon <http://steamcommunity.com/sharedfiles/filedetails/?id=439856500>`_ to you server's workshop collection for PS2 to work.

If you have not set up a server workshop collection, follow these steps:

#. **Generating a web api authorization key**: In order to use a workshop collection on your server, it must first have a web api authorization key. You can get one `here <http://steamcommunity.com/dev/apikey>`_. Once you have your key, add a new launch parameter to your srcds.exe command line: ``-authkey YOURAUTHKEYHERE``.

#. **Creating a workshop collection**: Next create a workshop collection `here <http://steamcommunity.com/workshop/editcollection/?appid=4000>`_. Select Server Content as Type and fill the rest of the fields. Next add the `Content Addon <http://steamcommunity.com/sharedfiles/filedetails/?id=439856500>`_. It's easier to find if you subscribe/fav it first.

#. **Publish the collection**: On the last page when creating the collection, click "Publish". You might have to agree to the Steam TOS to proceed. The URL of the collection should look something like this when you are finished: ``http://steamcommunity.com/sharedfiles/filedetails/?id=913621233``. Write down the numbers from the URL.

#. **Add the collection to your server**: Once you have written down the workshop id from the previous step, add a new launch parameter to your srcds.exe command line: ``+host_workshop_collection 123123123``, replacing the numbers with the id. Your launch parameters should now include both, the workshop collection and the authkey from step 1: ``+host_workshop_collection 123123123 -authkey YOURAUTHKEYHERE``.

Configuration
-------------
Pointshop2 requires no initial configuration! Once it is installed you are ready to go!
Restart your server and press F3 to open the menu.
You can find all settings under the "Management" tab.

If you don't see "Management" tab you either don't have administration addon or you are not admin.

If you already have addon such as ULX go to your server's console. You can access XGUI with either "!menu" chat command or ``xgui`` console command. I suggest binding XGUI to any key for quick access. Use ``bind x xgui`` in console to bind command. Replace x with your key.
If you don't have such addon installed download ULX and ULib from Github or add those to your server's workshop collection.
To add yourself as admin type ``ulx adduser *your name* superadmin``.

Advanced Configuration
----------------------

There are a few options in Pointshop2 that can be used to integrate the script more tightly into your system.

MySQL Setup
***********
By default SQLite (via sv.db) is used to store all player and pointshop data. If you have a MySQL server you can also use MySQL with the script. This has the advantage of being more efficient for large amounts of data, enabling you to share items across multiple servers and allowing you to display data on the web. 

If you want to switch from SQLite to MySQL you need to convert your database. We have created a tool where you can upload your SQLite database (located in your server's garrysmod folder) and download a .sql.gz file that you can import with phpmyadmin. `SQLite to MySQL <https://beta.pointshop2.com/sqlite-conversion/tool>`_

To enable MySQL please follow these steps:

#. **Install the gmsv_mysqloo module**: Download the module from `facepunch <https://facepunch.com/showthread.php?t=1515853>`_ and follow the installation instructions for your operating system at the bottom of the post.

#. **Enable MySQL within LibK**: LibK is used for all database operations of Pointshop2. To enable MySQL support go into the configuration file *addons/libk/lua/libk/server/sv_libk_config.lua*. Set ``LibK.SQL.UseMysql = true`` and update the remaining settings with your database connection details. If you are hosting the database on a different machine than the gamemserver, make sure to allow external connections to the database. 

#. **Test the configuration**: After a server restart Pointshop2 will now connect to MySQL. If there are any errors when connecting to the database they will be shown in the server console and logged to garrysmod/data/LibK_Error.txt serverside.


Troubleshooting and reporting bugs
----------------------------------

When you are experiencing issues with pointshop 2 please follow these steps. For a fast solution include as much information as possible. Report bugs and problems through `Discord <https://discord.gg/N9DmwwX>`_ #support channel.

#. **Turn on debug mode**: Follow the steps outlined here to enable verbose logging: :ref:`dev-options`.

#. **Create a minimal test case**: Try to reduce the steps needed to create the problem. Once you have found the quickest reliable way to create a problem note down the steps in a step by step fashion.

#. **Capture the load log**: When the script loads it outputs a lot of information to the console. In your report include this, from both server and client console. If something goes wrong during load other errors can happen. The load log is printed on connect (clientside) and after a map change (serverside).

#. **Include client and server console logs**: Include the client and server console logs from when the issue happens. Include a bit before and after, including too much is not a problem. Use a pastebin like http://hastebin.com/ for storing the information.

#. **Include server configuration**: Are you using MySQL or SQLite? Do you use any custom extensions or any DLC? Which administration mod do you use? Which gamemode do you run?

Importing and exporting items and categories
--------------------------------------------

Pointshop 2 allows importing and exporting items to text. You can use this feature to make backups of the shop or to transfer the item and category setup between servers.

Exporting and importing items can only be done trough lua commands. You can however run these through the server console by prefixing them with lua_run. Check :ref:`export-import`

Example workflow: 

.. highlight:: lua
.. code-block:: lua

	-- On Server 1:
		Pointshop2Controller:getInstance():exportItems() -- A filename is printed to the console
		Pointshop2Controller:getInstance():exportCategoryOrganization() -- A filename is printed to the console
		
	-- You would now go into the data directory and transfer files from the first to the second server
	
	-- On Server 2:
		Pointshop2Controller:getInstance():importItemsFromFile( "filename_1.txt" ) -- The filename from the first command
		Pointshop2Controller:getInstance():importCategoriesFromFile( "filename_2.txt" ) -- The filename from the second command


.. note::

   Graphical import/export features and importing/exporting of wallets and inventories is planned and will be added in a future update.
