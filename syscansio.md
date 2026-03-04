SYS Casino API Integration Guide
Welcome to the SYS Casino API documentation. This guide provides detailed instructions

for integrating SYS services into your application using your UUID and Secret Key.

Base URL
Prod - https://syscasino.com/

Testing - https://sys.xnet789.net/

Authentication & Signature Generation
Signature Generation Steps:

Convert request data into an array of key-value pairs.
Sort the array by keys in ascending order.
Generate a URL-encoded query string.
Create an HMAC-SHA1 signature using your secret key.
Example (JavaScript)
const generateSignature = (requestData, secretKey) => {

const dataArray = Object.entries(requestData);

dataArray.sort((a, b) => a[0].localeCompare(b[0]));

const queryString = dataArray.map(([key, value]) =>

${encodeURIComponent(key)}=${encodeURIComponent(value)}

).join("&");

const hmac = CryptoJS.HmacSHA1(queryString, secretKey);

return hmac.toString(CryptoJS.enc.Hex);

};

Request Format
{

"data": {

// your request payload

},

"sign": "generated_signature_here",

"uuid": "your_uuid_here"

}

Game List API
Fetch the list of available games.
Endpoint: /api/games/slot/app/games

Method: POST

Request Example
{

"data": {

"timestamp": 1749117303

},

"sign": "your_signature",

"uuid": "your_uuid"

}

Response
{

"status": "success",

"data": [

{

"id": 1,

"game_code": "28201",

"game_name": "Privé Lounge Roulette",

"provider_name": "Pragmatic Play Live",

"provider_code": "PPL",

"provider_category": "live-casino"

}

],

"meta": {

"total": 5032

},

"message": "retrieve game successfully"

}

Max Limit API
This API retrieves the maximum accepted limit to be used as unit_amount when launching

the game API. It is a public API and does not require authentication.

Endpoint : /api/games/slot/max-accept-limit

Method: GET

Launch Game API
Launch a game for a player.
Endpoint: /api/games/slot/launch

Method: POST

Request Example
{

"data": {

"game_code": "RICHWATER",

"provider_code": "ASKMEBET",

"player_id": "177" // max-length = 6 digits

"player_name": "player",

"unit_amount": 2000,

"transaction_id": "13458",

"redirect_url": "https://yourdomain.com/games",

"timestamp": 1749118563

},

"sign": "your_signature",

"uuid": "your_uuid"

}

Response
{

"status": "success",

"data": {

"url":
"https://games.askmeslot.io/games/richwater/v52/index.html?t=..."

},

"message": "get login url successfully"

}

Error Handling
The Launch Game API may return a 500 status code and handles specific error scenarios

with the following behavior:

Error Messages: ”Deposit failed”, ”Game not found”, ”Temporarily disabled” : If
the API error message contains any of these strings (even with extra text like
Deposit failed! Invalid Transaction), the game unit transfer has failed. Your system
should refund the user’s balance to reverse the transaction.
Error Message: ”Game is maintenance” : If the API returns this error message, the
game unit transfer was successful, and the user’s balance should not be refunded.
You can use the Withdraw API to retrieve the user’s balance if needed.
Player Balance API
Check a player's current balance.
Endpoint: /api/games/slot/player-balance

Method: POST

Request Example
{

"data": {

"player_id": "117",

"timestamp": 1749119228

},

"sign": "your_signature",

"uuid": "your_uuid"

}

Response
{

"status": "success",

"data": {

"Balance": 0,

"Message": "Success Operation"

},

"message": "get player balance successfully"

}

Withdraw API
Withdraw units from a player's balance.
Endpoint: /api/games/slot/withdrawl

Method: POST

Request Example
{

"data": {

"player_id": "177",

"unit_amount": 1477.5,

"transaction_id": "43434343",

"timestamp": 1749117303
},

"sign": "your_signature",

"uuid": "your_uuid"

}

Response
{

"status": "success",

"data": {

"amount": 1000

},

"message": "Withdraw successfully"

}

Win/Lose History API
Retrieve win/lose history for players.
Endpoint: /api/games/slot/win-lose-history

Method: POST

Request Example
{

"data": {

"timestamp": 1734853272

},

"sign": "your_signature",

"uuid": "your_uuid"

}

Response
{

"status": "success",

"data": [

{

“id”:1,

"player_id": 12597,

"game_type": "slot",

"stake": 100,

"player_win_loss": -100,

"metadata": "{"GameName":"Elf Bingo","GameCode":"172"}"

}

],

"message": "fetch win/lose successfully"

}

Approved Win/Lose Report API
This API allows you to confirm specific win/lose records (by winLoseIds) to SYS. It
tells SYS that these records have been successfully copied to your system.
Endpoint: /api/games/slot/approved

Method: POST

Request Example
{

"data": {
"timestamp": 1734853272,

"winLoseIds": [1, 2, 3, 4, 5] //id from Win/Lose History API

},

"sign": "your_signature",

"uuid": "your_uuid"

}

Response
{

"status": "success",

"data": [

{

"id": 1,

"player_id": 12597,

"game_type": "slot",

"stake": 100,

"player_win_loss": -100,

"metadata": "{"GameName":"Elf Bingo","GameCode":"172"}"

}

],

"message": "fetch approved win/lose successfully"

}

🚫 Disabled Game & Provider List API
This API provides a list of temporarily disabled games and providers from the SYS
platform. It is useful for agents or platforms to dynamically filter out unavailable
content from their frontend or game launch logic.
Endpoint: /api/games/slot/disabled-list

Method: GET

❌ Error Response
HTTP Status Code : 500 Internal Server Error
{

"status": "error",

"errors": [],

"message": "Invalid Sign!"

}