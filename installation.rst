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

"UnlitGeneric"
{
	"$basetexture" "trails/dollar"
	"$vertexalpha" 1
	"$vertexcolor" 1
}

To get your image to an actual Pointshop item, go to the second tab called Management. Now you should be on a tab called 'Create Items', with options to select the type. Go to Trail to bring up the basic settings menu, where you can personalize the item you are going to make. Once you are happy with the name and price, click the image preview next to the file path. This will bring up a box displaying all functioning materials inside /trails. Hover over them to play an animated preview, which will give some indication of how they look in-game. Once happy, save the item and if successful, will be found in Uncategorised Items, located inside the Manage Items tab. The last step is to move it into a category, which can achieved via drag and drop.

FastDL
============
Unless players already have the files from other places, they will see errors or texture problems if there is no FastDL system. If you haven't already set this up, see here (http://maurits.tv/data/garrysmod/wiki/wiki.garrysmod.com/index70e8.html)