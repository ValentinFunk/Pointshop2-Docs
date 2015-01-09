Getting and Setting player points
=================================

In Pointshop 2 points are stored in a player's wallet (:lua:class:`Wallet`). A wallet is a table that contains points and premiumPoints.

Wallets are only networked to their owner and to all admins by default. If you want to display points on a scoreboard, you need to tick the setting "Broadcast Wallets" in the General Settings. This will send everyone's wallet to everyone.

Use ply.PS2_Wallet to access a player's wallet. To manipulate a wallet use

:lua:func:`PLAYER:PS2_AddPremiumPoints`

:lua:func:`PLAYER:PS2_AddStandardPoints`

There is also a console command available to give points to a specific steamid. You can use this with your donation system:

.. lua:function:: ps2_addpoints <steamId> <currencyType> <points>

    Gives points to a specific SteamID. Works even if the player has never joined the server.
    
    **steamId**: SteamID of the player in the STEAM_x_x:xxxxxxxxxx format
    
    **currencyType**: Currency to give. Can be points or premiumPoints
    
    **points**: Amount of points to give
