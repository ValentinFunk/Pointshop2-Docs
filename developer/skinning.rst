Creating Pointshop Skins
========================

Pointshop 2 skins are implemented as derma skins. This means that the Paint functions
of Panels are passed to a skin. If you are creating a skin you cannot overwrite or modify
any of the files but have to do your skinning entirely through a skin.

The name of the skin which is used is set within the main configuration file at 
*lua/ps2/shared/sh_config.lua*. The default flatui skin can be found in *lua/ps2/client/cl_dermaskin_flatui.lua*.
The inventory is seperately skinned through the skin configured in *lua/kinv/shared/sh_config.lua*, the default skin can be found in *lua/kinv/client/cl_dermaskin.lua*

Example Skins
-------------
- Blur Skin by AlphaWolf: https://github.com/snowywolf/Pointshop-2-Skin

Types of Hooks
--------------
There are two types of hooks that you can use to customize looks and behaviour:

#. **Layout Hooks**: These are always called after initialization of the component. You can use this hook to replace components with custom components or to reposition components.
#. **Paint Hooks**: These work like the normal panel:Paint hooks, use this to customize the appearance of the different panels.

If you are missing a hook on a component that you want to customize, please send Kamshak a pm on scriptfodder.

Fonts
-----
Fonts are defined as skin properties and can be customized through a custom skin as well.
