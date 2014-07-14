Installation
============
To install Pointshop2 simply extract the zip you downloaded into the addons folder.

Configuration
=============
Pointshop2 requires no initial configuration! Once it is installed you are ready to go!
Restart your server and press F3 to open the menu. If nothing happens, use the "pointshop2" console command.
You can find all settings under the "Management" tab.

Trails
============
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

FastDL
=============
Unless players already have the files from other places, they will see errors or texture problems if there is no FastDL system. If you haven't already set this up, see here http://maurits.tv/data/garrysmod/wiki/wiki.garrysmod.com/index70e8.html. As well as this, you must have an accompanying file dedicated to resource.AddFile.

PAC
=============
As well as the ordinary single prop-based hats you'll find in any Pointshop, here you also have the ability use PAC. First of all, grab the addon from the Workshop, here: http://steamcommunity.com/sharedfiles/filedetails/?id=104691717. Once it's installed, load up Garry's Mod in sandbox and press c (or whatever key is bound to open the context menu). Underneath the small button to change your player model, you'll find another that opens up the PAC editor. 

In short, PAC is an addon that allows you to build costumes out of props and various other tools available, such as lighting, particles and even text. To use it, you choose a prop from the sandbox spawn menu, use sliders to move it into a location you're happy with and repeat until finished. The first thing you'll want to do after installing is turning on advanced features. Do this by going to third tab, options, and hitting the second part down, you'll then have easy access to everything.

From here, what you make with PAC is entirely up to you, so it's recommended to just play around until you feel familiar. One aspect that makes costume creation a lot easier is the ability to t-pose your model, meaning they do not move around which can cause issues getting positions exactly right. Access this via the fourth tab, players. It's the first button and can be changed upon demand, if you wish to preview your costume in an animated manner. 

When working on PAC items that are not head-based, it is vital to change the bone to one that correctly suits the position of your costume. For example, if you are placing a model on the player's chest, go the orange orientation tab of PAC and click the button for it, which will bring up a list of bones that the prop can be attached to. In this scenario, you would click 'chest' or 'amulet' although it will really depend on what you are making. Failure to do so will usually cause costumes to fall out of place when moving around or in different standing positions. 

Item Creator
=============
One of the main features of Pointshop2 is to make item creation much easier and fluid.

Slots
=============
To avoid clipping and keep everything organized, items are categorized by different slots, which can be viewed via the inventory tab. This allows for multiple accessories on the player, such as head, pets, etc. Items are not set to a single slot, meaning they can be used in multiple areas if the user wishes to do so. 

Icons
=============