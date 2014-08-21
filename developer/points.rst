Getting and Setting player points
=================================

In Pointshop 2 points are stored in a player's **wallet**(:lua:class:`Wallet`). A wallet is a table that contains points and premiumPoints.

Use ply.PS2_Wallet to access a player's wallet. To manipulate a wallet use

:lua:func:`PLAYER:PS2_AddPremiumPoints(points)`

:lua:func:`PLAYER:PS2_AddStandardPoints(points)`