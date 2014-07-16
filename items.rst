Item Creation
=============

Trail Creation
--------------
The pointshop comes with a few trails readily available and it is very easy to add your own. If you wish to do this, simply place the files inside materials/trails and as long as this is correct, they will be picked up. When making your own, it is recommended to use a size of 128x128 and in VTF format, as .png can lead to crashes. When handling the .VMT, use these specifics to avoid blurring or blocky previews:

.. highlight:: lua
.. code-block:: lua

 "UnlitGeneric"
 {
 "$basetexture" "trails/dollar"
 "$vertexalpha" 1
 "$vertexcolor" 1
 }

To get your image to an actual Pointshop item, go to the second tab called Management. Now you should be on a tab called 'Create Items', with options to select the type. Go to Trail to bring up the basic settings menu, where you can personalize the item you are going to make. Once you are happy with the name and price, click the image preview next to the file path. This will bring up a box displaying all functioning materials inside /trails. Hover over them to play an animated preview, which will give some indication of how they look in-game. Once happy, save the item and if successful, will be found in Uncategorised Items, located inside the Manage Items tab. The last step is to move it into a category, which can achieved via drag and drop.


Accessory/Hat Creation
----------------------
Hats in pointshop2 are PAC3 items. As well as the ordinary single prop-based hats you'll find in any Pointshop, here you also have the ability use PAC. This allows you to create animated hats, add particles, position hats interactively onto different models and even create full armor or accessories. This can all be done without any lua knowledge and allows you to easily create hats that are absolutely unique to your server. 

When creating a hat you have two options:

#. Using the ordinary PAC3 editor and importing the outfits into Pointshop 2

#. Using the PAC3 editor embedded within the Pointshop2 hat editor

Generally it is recommended to use the second way, this allows you to use the full editor and gives you more options. A common approach is to first create the PAC outfits in sandbox and then use the Hat Creator within the Management Tab to create a pointshop item from it. In gamemodes that do not derive from sandbox (for example TTT or Murder) the PAC editor cannot be used. In this case you can still use the Pointshop2 Hat Editor to create and position hats.

Introduction into PAC
*********************
PAC (short for Player Appearance Customizer) is an addon made by CapsAdmin. It allows you to fully customize your looks.

First of all, grab the addon from the Workshop `here <http://steamcommunity.com/sharedfiles/filedetails/?id=104691717>`_. Once it's installed, load up Garry's Mod in sandbox and press c (or whatever key is bound to open the context menu). Underneath the small button to change your player model, you'll find another that opens up the PAC editor.

In short, PAC is an addon that allows you to build costumes out of props and various other tools available, such as lighting, particles and even text. To use it, you choose a prop from the sandbox spawn menu, use sliders to move it into a location you're happy with and repeat until finished. The first thing you'll want to do after installing is turning on advanced features. Do this by going to third tab, options, and hitting the second part down, you'll then have easy access to everything.

From here, what you make with PAC is entirely up to you, so it's recommended to just play around until you feel familiar. One aspect that makes costume creation a lot easier is the ability to t-pose your model, meaning they do not move around which can cause issues getting positions exactly right. Access this via the fourth tab, players. It's the first button and can be changed upon demand, if you wish to preview your costume in an animated manner.

When working on PAC items that are not head-based, it is vital to change the bone to one that correctly suits the position of your costume. For example, if you are placing a model on the player's chest, go the orange orientation tab of PAC and click the button for it, which will bring up a list of bones that the prop can be attached to. In this scenario, you would click 'chest' or 'amulet' although it will really depend on what you are making. Failure to do so will usually cause costumes to fall out of place when moving around or in different standing positions.


Further information, tutorials and example items:

- `The official Facepunch thread <http://www.facepunch.com/showthread.php?t=1251238>`_
- `The official Github repository <https://github.com/CapsAdmin/pac3>`_
- `PAC3 Beginners FAQ <https://github.com/CapsAdmin/pac3/wiki/Beginners-FAQ>`_
- `Tutorials and information <https://github.com/CapsAdmin/pac3/wiki>`_

The Accessory/Hat Maker
***********************
One of the main features of Pointshop2 is to make item creation much easier and fluid.
The Accessory/Hat Maker is the tool used to create PAC3 powered Hats and Accessories. This includes Pets, Hats and various other items that modify the look of the player.

The editor can be accessed within the Management tab under "Create Items". Select Accessory/Hat and the editor will open. To create an item follow these steps:

#. **Fill out the basic information**: Fill out the basic fields such as name, point costs and a description.

#. **Create or import the base outfit**: To do this, simply click on the Open Editor button and select the respective option. This outfit is applied to all models by default. CS:S Playermodels usually require slightly different positioning of the items.

#. **Add model specific outfits**: To modify the item positions for CS:S or other playermodels, click the "Add" button beneath the main editor button. You can now choose to create an outfit for all CS:S models or choose a model manually. After selecting this option you can clone the base outfit and adapt the positions. Please not that the outfit is only cloned when you click this button, if you change the main outfit after cloning the changes will not automatically apply to all model specific outfits. In order to fix this simple reclone the outfit by selectiong the option within the model specific outfits table.

#. **Create a shop icon**: Icons for PAC items are automatically generated. To specify from where the icon should look at the item you can use the icon editor. Within the item positioner you will usually click on the "Icon Snapshot" button. This will initialize the icon for you. To fine tune the icon's view you can use the sliders next to the icon.

#. **Create an inventory icon**: To update the inventory icon follow the same procedure as for the shop icon. Please note that creating a new icon snapshot will overwrite previous changes. It is recommended that you use the sliders for the inventory icon after creating the shop icon.

Slots
*************
To avoid clipping and keep everything organized, items are categorized by different slots, which can be viewed via the inventory tab. This allows for multiple accessories on the player, such as head, pets, etc. Items are not set to a single slot, meaning they can be used in multiple areas if the user wishes to do so. 

To assign an item to a slot simply check the checkboxes in the item editor. Only slots that were created for Accessory/Hat items can be used, so a PAC item cannot be put into a Trail slot. 
