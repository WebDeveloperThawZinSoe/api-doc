Buffalo Game Seamless Integration - API Documentation
Key Integration Rules
Game Launch:

First, request a game URL from our API.
Open it for the player.
Server → Server Logs:

We send a log every spin/round.
You must reply { "status": "ok" } immediately, or the round is terminated.
Balance Lock:

Lock the player’s balance while playing.
On round end, we send exitInfos, so you can unlock those users.
Game Environment
Purpose	Method	Endpoint
Game Launch URL	POST	https://api4.qianxu168.com/game/url
Game Report Detail by TransactionID	POST	https://api4.qianxu168.com/inspect.php
Game Launch
Request a launchable game URL, then open it in your player’s browser/iframe.

Request Body
{
  "id": "bf10799901",
  "game": "AfricanBuffalo",
  "domain": "buffalo688",
  "balance": 5007
}
Response Body
{
  "status": "ok",
  "players": [
    {
      "playerId": "bf123455",
      "balance": 1000.35
    }
  ]
}
Open the game URL for the player after a successful response. The players array can include multiple players if needed.

Game Report Detail (by TransactionID)
Fetch round details for a specific transactionId (useful for BO/CS).

Request Body
{
  "domain": "buffalo688",
  "transactionId": "1757263203983752334"
}
Response Body
The response shape depends on the provider's detail format. Use it for round diagnostics/verification.

Round-End Webhook (Sent to Your Server)
On each round end, we POST a log to your webhook. You must ACK with { "status": "ok" }.

Payload Schema
{
  "detail": {},
  "domain": "buffalo688",
  "exitInfos": [
    {"id": "buffalo1183"},
    {"id": "buffalo11822"}
  ],
  "game": "AfricanBuffalo",
  "matchNo": 34424110,
  "reportId": 1760357702072694000,
  "transactions": [
    {
      "amount": -80,
      "balance": 2075,
      "bet": 80,
      "commission": 0,
      "id": "buffalo1183768",
      "playerType": "",
      "status": "lose",
      "transactionId": 1760357702072700000
    }
  ]
}
Processing Rules (Your Side)
For each transactions[] item:

new_balance = old_balance + amount.
Persist transactionId as your round ID for BO checks.
Unlock all users listed in exitInfos.
ACK with:
{
  "status": "ok",
  "players": [
    {
      "playerId": "bf123455",
      "balance": 1000.35
    }
  ]
}
If you don’t ACK, we terminate the round.

Balance Locking Behavior
Set a strict lock when the user launches a Buffalo game (block withdrawals/transfers/other updates).
Only apply changes from our webhook logs during play.
Release the lock for all users listed in exitInfos at round end.
RTP Configuration
You can configure Return to Player (RTP) per agent. Without per-agent RTP, a global RTP applies.

© 2025 Buffalo Games – Game Environment.