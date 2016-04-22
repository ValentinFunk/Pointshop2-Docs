Getting and Setting player points
=================================

In Pointshop 2 points are stored in a player's wallet (:lua:class:`Wallet`). A wallet is a table that contains points and premiumPoints.

Wallets are only networked to their owner and to all admins by default. If you want to display points on a scoreboard, you need to tick the setting "Broadcast Wallets" in the General Settings. This will send everyone's wallet to everyone.

Use ply.PS2_Wallet to access a player's wallet. 


.. highlight:: lua
.. code-block:: lua
	
	local points, premiumPoints = 0, 0
	if ply.PS2_Wallet then
		points, premiumPoints = ply.PS2_Wallet.points, ply.PS2_Wallet.premiumPoints
	end
	print( points, premiumPoints )

To manipulate a wallet use

:lua:func:`PLAYER:PS2_AddPremiumPoints`

:lua:func:`PLAYER:PS2_AddStandardPoints`

There is also a console command available to give points to a specific steamid. You can use this with your donation system:

.. lua:function:: ps2_addpoints <steamId> <currencyType> <points>

    Gives points to a specific SteamID. Works even if the player has never joined the server.
    
    **steamId**: SteamID of the player in the STEAM_x_x:xxxxxxxxxx format
    
    **currencyType**: Currency to give. Can be points or premiumPoints
    
    **points**: Amount of points to give

Getting via MySQL (for loadingscreens etc)
******************************************
To get a player's points from a pointshop2 mysql database you can use the following query:

.. highlight:: sql
.. code-block:: sql

	SELECT w.points AS points, w.premiumPoints AS premiumPoints
	FROM ps2_wallet w, libk_player p
	WHERE w.ownerId = p.id
	AND p.player =  "STEAM_0:0:19299911"

To get points via steamid64 you can use this query:

.. highlight:: sql
.. code-block:: sql

	SELECT w.points AS points, w.premiumPoints AS premiumPoints
	FROM ps2_wallet w, libk_player p
	WHERE w.ownerId = p.id
	AND p.steam64 =  "76561197998865550"

The result row of these queries will contain a points and premiumPoints collumn.

Giving Items
============
 
To give an item to a player you can use

.. lua:function:: PLAYER:PS2_EasyAddItem( itemClassName, purchaseData, suppressNotify )

    Gives an item to the player.
    
    **itemClassName**: Class name of the item
    
    **purchaseData**: [OPTIONAL] A table in the format { time = os.time(), amount = 123, currency = "points", origin = "LUA" }. amount is a number, currency can be "points" or "premiumPoints". This is used to calculate the sell price of the item. Origin is a string to track how the item was given. It has no set format.
    
    **suppressNotify**: [OPTIONAL] If set to true the "New Item Received" popup doesn't show up.

Examples
********

In these examples please note that there can be multiple items with the same print name. It is better to give an item by class name. To determine the class name you either look at the database directly (className is the persistence id of the item) or use PrintTable(Pointshop2.GetRegisteredItems())

.. highlight:: lua
.. code-block:: lua

	/*
	 *	Gives a random item from the shop to a player
	 */
	function GiveRandomItem( ply )
		local items = Pointshop2.GetRegisteredItems( )
		local itemClass = table.Random( items )
		return ply:PS2_EasyAddItem( itemClass.className )
	end
	GiveRandomItem( player.GetByID( 1 ) )

	/*
	 *	Gives a item with the specified name to the player
	 */
	function GiveItemByPrintName( ply, printName )
		local itemClass = Pointshop2.GetItemClassByPrintName( printName )
		if not itemClass then
			error( "Invalid item " .. tostring( printName ) )
		end
		return ply:PS2_EasyAddItem( itemClass.className )
	end
	GiveItemByPrintName( player.GetByID( 1 ), "Gas Mask" )
