Module Creation
---------------

Modules are the best way to extend pointshop. Through them new item creators can 
be added.

Structure
*********
The module structure is very simple. Each module is a folder within the *lua/ps2/modules* folder.
Every file in this folder is recursively loaded by the module loader. The realm is determined by
the file prefix (sh, cl, sv). Client files are automatically AddCSLuaFile'd. 

.. function:: Poinsthop2.RegisterModule( MODULE )

   Describes a Python function.

Within this folder the module description file *sh_module.lua* needs to be placed.
Here you set up the module table which contains information such as the author and name of the module, then register it using :lua:func:`Pointshop2.RegisterModule`.