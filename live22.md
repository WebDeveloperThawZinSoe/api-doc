
Table of Contents.........................................................................................................................2
Version Control............................................................................................................................5
- API Overview............................................................................................................................8
1.1 Seamless Wallet API.........................................................................................................8
1.2 Fund Transfer API..............................................................................................................8
1.3 Integration API...................................................................................................................9
1.3.1 Free Round Feature Integration API.........................................................................9
1.4 Player ID..........................................................................................................................10
1.5 Game Session.................................................................................................................10
1.5.1 Bet and Game Result..............................................................................................10
1.5.2 Transaction IDs.......................................................................................................10
1.5.3 AuthToken...............................................................................................................10
1.6 Data Retention Policy......................................................................................................10
- Integration API.......................................................................................................................11
2.1 API Documentation..........................................................................................................12
2.1.1 POST GetGameList................................................................................................12
2.1.2 POST GameLogin...................................................................................................14
2.1.3 GET LaunchGame..................................................................................................16
2.1.4 POST GetTransactionDetails..................................................................................17
2.1.5 POST GetDaySummary..........................................................................................19
2.1.6 POST KickPlayer....................................................................................................20
2.1.7 POST GetUnfinishRound........................................................................................21
2.1.8 POST CancelRound...............................................................................................23
2.1.9 POST SettleRound.................................................................................................24
2.1.10 POST GetRoundDetails........................................................................................26
2.2 Demo Launch Game........................................................................................................28
2.2.1 GetGameList and GameLogin method...................................................................28
2.2.2 GET GameList........................................................................................................28
2.2.3 GET LaunchGame..................................................................................................28
2.3 Free Round Feature Integration API................................................................................29
2.3.1 POST CreateFreeRound........................................................................................29
2.3.2 POST CancelFreeRound........................................................................................31
2.3.3 POST GetFreeRoundInfoByPlayer.........................................................................32
2.3.4 POST GetFreeRoundGames..................................................................................34
2.3.5 POST GetFreeRoundDetails..................................................................................36
2.3.6 POST GetFreeRoundInfoByOperator.....................................................................38
- Seamless Wallet Integration API..........................................................................................41
3.1 Game Opening Method...................................................................................................41

3.2 API Documentation..........................................................................................................42
3.2.1 POST GetBalance..................................................................................................42
3.2.2 POST Bet................................................................................................................43
3.2.3 POST GameResult.................................................................................................45
3.2.4 POST Rollback.......................................................................................................47
3.2.5 POST CashBonus...................................................................................................49
3.2.7 POST BetNSettle....................................................................................................52
3.2.8 POST CancelBetNSettle.........................................................................................54
3.3 Flow of placing bets for seamless....................................................................................57
- Fund Transfer Wallet Integration API...................................................................................58
4.1 Game Opening Method...................................................................................................58
4.2 API Documentation..........................................................................................................59
4.2.1 POST CreatePlayer................................................................................................59
4.2.2 POST CheckBalance..............................................................................................60
4.2.3 POST Deposit.........................................................................................................61
4.2.4 POST Withdraw......................................................................................................62
4.2.5 POST PullLog.........................................................................................................64
4.2.6 POST FlagLog........................................................................................................66
4.2.7 POST PullLogByTimestamp...................................................................................67
4.2.8 POST PullLogBonus.....................................................................................................70
4.2.9 POST FlagLogBonus..............................................................................................73
4.2.10 POST PullLogBonusByTimestamp.......................................................................74
4.2.11 POST CheckTransferStatus..................................................................................77
4.3 Transaction Log Pulling Mechanism................................................................................79
4.4 Log Pulling by Timestamp Mechanism............................................................................80
- Reconciliation........................................................................................................................82
5.1 Bet Transaction................................................................................................................82
5.2 Rollback Transaction.......................................................................................................82
5.3 Game Result Transaction................................................................................................82
5.4 Bonus Transaction...........................................................................................................82
- MD5 Hashing..........................................................................................................................84
6.1 For C#..............................................................................................................................84
6.2 For Javascript..................................................................................................................85
6.3 For PHP...........................................................................................................................85
6.4 For Python.......................................................................................................................85
6.5 For Bash..........................................................................................................................86
6.6 For Ruby..........................................................................................................................86
6.7 For Java...........................................................................................................................87
6.8 For Swift...........................................................................................................................88
6.9 For Kotlin.........................................................................................................................88
- Appendix................................................................................................................................90

7.1 Supported Language Code..............................................................................................90
7.2 Supported Currency Code...............................................................................................91
7.3 Status / Error Code..........................................................................................................92
7.3.1 Status Code from Provider......................................................................................92
7.3.2 Status Code from Operator.....................................................................................93
7.4 Game Type (Game Category).........................................................................................93
7.5 Game Result Type...........................................................................................................94
7.6 Rollback Type..................................................................................................................94
7.7 Round Type.....................................................................................................................94
7.8 Transaction Type.............................................................................................................94
7.9 Bonus Type......................................................................................................................94
8.0 Result...............................................................................................................................94


## Version Control

Version  Description Modified by Date
V1.0 -First Release Jack 12 Jan 2023
V2.0 -Remove buyin, buyout, pushedresult operator API
-GetGameList response format updated
WL 28 Feb 2023
V2.1 Update ReturnStatus code from Provider WL 14 Mar 2023
## V2.2
-Add game login sequence diagram
-Add bet result sequence diagram
## Jack 19 May 2023
## V2.3
-Add GetTransactionDetails Provider API
-Return Duplicate Transaction Response Status code on Deposit
and Withdraw API
WL 29 May 2023
V2.4 -Update Supported Currency Code Jery 5 June 2023
V2.5 -Update md5 hashing detail implementation Jack 12 June 2023
V3.0 -Combine both seamless and fund transfer into 1 documentation
-Create section for 3 different purposes API (Generic, Seamless
and Fund Transfer)
-Add missing information about game session behaviour,
transaction id uniqueness, player id requirement, etc.
-Update auth token field in game login, and other seamless
callback request
-Add day summary API
-Add sequence diagram and details step for log pulling
mechanism
-Add reconciliation definition
## Jack 21/08/2023
V3.1 -Add demo games integration method 2.2

-Add environment ip address for whitelisting
## - Jack 05/09/2023
V3.2 -Add Free Round Feature API - WL 07/09/2023
V3.2.1 -Update Free Round Feature API GetFreeRoundGames Response  - WL 19/09/2023
V3.2.2 -Add 2.2.2 GET GameList, GET request to retrieve demo only
gamelist
-Add 7.5 Game Result Type and 7.6 Rollback Type
## All Wallet Jack 29/09/2023
V3.2.3 -CashBonusAPI tranId type change to String(25) Seamless Jack 06/10/2023
V3.3.1 -Add 2.1.5 POST KickPlayer API to kick player from game
-Add 2.1.6 POST GetUnfinishedRound
-Add 2.1.7 POST CancelRound
## All Wallet Jack 16/10/2023
V3.3.2 -Remove AuthToken request field on Seamless API (GameResult,
Rollback, and CashBonus)
Seamless WL 03/11/2023
V3.3.3 -Add 2.1.8 GetRoundDetails  All Wallet WL 17/11/2023
V3.3.4 -Modify 2.1.8 GetRoundDetails  Response All Wallet WL 12/12/2023
V3.3.4 -Modify 2.1.8 GetRoundDetails  Response All Wallet WL 12/12/2023
v3.3.5 -Modify 2.1.6 GetUnfinishRound Response All Wallet Kai Neng 18/12/2023

v3.3.6 -Add 4.2.7 PullLogByTimestamp
-Add 4.4 Log Pulling by Timestamp Mechanism
## Transfer  Jack 09/01/2024
v3.3.7 -Modify 2.1.8 GetRoundDetails  Response
-Modify 2.3.5 GetFreeRoundDetails  Response
-Modify 3.2.2 Bet  Response
-Modify 3.2.3 GameResult  Response
-Modify 3.2.4 Rollback  Response
-Modify 3.2.5 CashBonus  Response
-Modify 3.2.7 BuyIn  Response
-Modify 3.2.8 BuyOut  Response
-Modify 3.2.3 UpdateGameResult  Response
-Modify 4.2.5 PullLog  Response
-Modify 4.2.7 PullLogByTimestamp  Response
All Wallet KB 17/01/2024
v3.3.8 -Add RoundType on 3.2.3 GameResult  Request
-Add RoundType on 4.2.5 PullLog, 4.2.7 PullLogByTimestamp
## Response
All Wallet WL 18/01/2024
v3.3.9 -Add Pull log bonus Api on 4.2.8 POST PullLogBonus,4.2.9 POST
FlagLogBonus, 4.2.10 POST PullLogBonusByTimestamp
-Modify TranDT format in Response to UTC format on 2.3.5 POST
GetFreeRoundDetails, 4.2.5 POST PullLog, 4.2.7 POST
PullLogByTimestamp, 4.2.8 POST PullLogBonus,  4.2.10 POST
PullLogBonusByTimestamp
## All Wallet Martin 19/7/2024
v3.4.0 -Add Check Transfer status Api on 4.2.11 POST
CheckTransferStatus
## Fund Transfer Martin 23/08/2024
v3.4.1 -Add Settle Round Api on 2.1.8 POST SettleRound All Wallet Martin 02/09/2024
v3.4.2 -Add new request body on 2.1.9 GetRoundDetails  All Wallet KB 25/09/2024
v3.4.3 -Add 2.3.6 GetFreeRoundInfoByOperator
-Modify 3.2.5 CashBonus  Request (Add BonusType)
-Modify 2.3.4 GetFreeRoundGames Response(Add
MaxSpinCountCap & MaxWinCapMultiplier)
All Wallet SH 15/10/2024
v3.4.4 -Deprecated Buyin/BuyOut/UpdateGameResult API for legacy
fish arcade integration
## Seamless Martin 30/10/2024
v3.4.5 -Operator callback response time update
-Modify 3.3 Flow of placing bets for seamless
-CreateFreeRound condition update
-Modify 2.3.1 POST CreateFreeRound
-Data Retention policy
-Modify 1.6 Data Retention Policy
-Modify 2.1.3 POST GetTransactionDetails
-Modify 2.1.7 POST CancelRound
-Modify 2.1.9 POST GetRoundDetails
-Auth token usage
-Modify 1.5.3 AuthToken
## All Wallet Martin 18/11/2024
v3.4.6 -Modify 2.3.6 GetFreeRoundInfoByOperator (Add pagination in
this API)
All Wallet SH 06/01/2025
v.3.4.7 -Add 8.0 Result
-Modify 3.2.5 CashBonus,  4.2.8 POST PullLogBonus and 4.2.10
POST PullLogBonusByTimestamp
All Wallet SH 14/1/2025
v3.4.8 -Modify 1.6 Data Retention Policy All Wallet Martin 27/1/2025
v3.4.9 -Modify 4.2.3 POST Deposit , 4.2.4 POST Withdraw All Wallet SH 7/4/2025

v3.5.0 -Add 2.2.3 GET LaunchGame

-Modify 2.1.1 POST GetGameList
## All Wallet Toh 8/72025
V3.5.1 -Add 3.2.7 POST BetNSettle , 3.2.8 POST CancelBetNSettle
-Add error code at 7.3 Status / Error Code
## Seamless Martin 15/7/2025
V3.5.2 - Modify 4.2.3 POST Deposit Amount param’s description
- Modify 4.2.4 POST Withdraw Amount param’s description

Fund Transfer KB 1/8/2025
V3.5.3 - Modify 3.2.5 CashBonus  example

Seamless KB 1/8/2025


- API Overview
1.1 Seamless Wallet API
Operator is expected to seamlessly integrate the Wallet Integration API into their platform. As a game
provider for online casinos, operators will be responsible for invoking the provided methods whenever
players place bets or achieve wins. This interaction with the API ensures that player balances are
accurately updated in accordance with their gaming activity.


## Method / Endpoint /
## Function
## Description Status
GetBalance This function facilitates the retrieval of a player's current balance. Required
Bet Checks if the player has enough funds and subtracts money from the player's
balance. Returns the value of updated balance.
## Required
GameResult Completion of a game round, the winning amount is added to the player's
balance, reflecting the conclusion of gameplay. The updated balance value is
returned.
## Required
Rollback In the event of a bet cancellation due to an unfinished game, this method
refunds the player's balance.
## Required
CashBonus Implemented in provider campaigns, tournaments, and cash drops, this method
informs the operator about a player's bonus winnings, leading to an increase in
the balance.
## Required
**REMARK: These APIs are exclusively intended for seamless wallet integration.

1.2 Fund Transfer API
The operator is empowered to leverage this API for facilitating fund transfers to players' balances within
the Game Provider's wallet ecosystem.

## Method / Endpoint /
## Function
## Description Status
CreatePlayer This method allows registering a new player on the provider system.

-The functionality is now deemed optional, as the CheckBalance and
GameLogin methods will inherently generate a player profile within the
provider's system if one does not already exist.
## Optional
CheckBalance This method can get the current balance of the player in the provider system. Required
Deposit This method transfers funds into the player's balance within the provider
system.
## Required
Withdraw This method transfers funds out of the player’s balance within the provider
system.
## Required
PullLog Using this method, the operator gains the capability to retrieve players betting
logs for fund transfer wallets..
## Optional
FlagLog Using this method, the operator gains the capability to flag retrieved records,
This action serves to prevent return of identical sets of betting logs when
invoking the PullLog method.
## Optional

**REMARK: These APIs are exclusively intended for fund transfer wallet integration.
1.3 Integration API
The Integration API provides a set of versatile methods that enable Operators to access the provider's
game list, initiate game launches, retrieve statistics, and perform other related actions.

## Method / Endpoint /
## Function
## Description Status
GetGameList Through this method, the operator gains the capability to retrieve a
collection of accessible games from the provider's system.
## Optional
GameLogin The operator invokes this method to obtain the game launch link. Required
GetTransactionDetails The operator employs this method to procure a report link presenting
comprehensive transaction details by utilising the game result id.
## Optional
GetDaySummary This method is designed to furnish a summarised overview of daily
transactions, categorised by currency.
## Optional
KickPlayer The operator invokes this method to temporary kick player from continuing
playing the game
## Optional
GetUnfinishRound The operator invokes this method to retrieve list of unfinished game rounds
held by player
## Optional
CancelRound This method is designed to allow operators to cancel a game round based
on its round ID.
## Optional

1.3.1 Free Round Feature Integration API
The Free Round Feature API is a marketing tool used by operators to offer players free gameplay
sessions. Operators create and manage these sessions to attract and retain players, customise
promotions, and monitor their impact on the platform. This feature helps boost player engagement and
loyalty.

## Method / Endpoint /
## Function
## Description Status
CreateFreeRound Operators may utilise this method to grant players complimentary rounds in
a variety of games.
## Optional
CancelFreeRound Method that enables operators to revoke or nullify a previously granted free
round.
## Optional
GetFreeRoundInfoByPlayer This method allows operators to access detailed information about player's
free rounds, aiding in better player management and engagement.
## Optional
GetFreeRoundGames Retrieve a list of game information that are eligible for free rounds. Optional
GetFreeRoundDetails Retrieve all transaction information for a specific free round. Optional


1.4 Player ID
Player ID (PlayerId parameter) is a unique identifier of the user within the operator system. Before
sending to the provider any gaming related request operator must create it first and store it somewhere
inside the operator system. If a player is new and its account does not exist in the provider system it will
be created automatically on the base of the data sent by the operator server in the (CreatePlayer,
GameLogin) request. If a player account already exists in the provider database it will be updated with the
request data if necessary. Player id received in the provider system will be sent with all subsequent
requests to the operator system.

The provider's system Player Id field has a character limit of 50. It's advised to avoid sending more
characters than the specified limit.
## 1.5 Game Session
1.5.1 Bet and Game Result
In the context of the bet and game result methods, each game round will encompass a solitary instance of
a bet, game result, or refund for the bet.
1.5.2 Transaction IDs
The Transaction ID, utilised in bets, game results and cash bonuses, maintains its uniqueness across the
entirety of the provider's gaming system.
1.5.3 AuthToken
The operators are able to pass in AuthToken during gamelogin and achieve session control through
callback. AuthToken will be pass back to operator through (Getbalance, Bet callback only)
**REMARK: This is only applicable for seamless operators, for fund transfer they may opt to use Kickplayer API.


## 1.6 Data Retention Policy
## 1.6.1 Real-time Transaction

-Transactions will be retained for
30 days.
-Outstanding transactions/unsettled rounds will be settled after 1 hour.
1.6.2 Operator Log pulling
-Log pulling transaction data will be retained for 60 days.
-All transaction data that exceeds the above-mentioned data retention periods will be archived
and will no longer be visible on the back office.


- Integration API
This collection comprises a set of versatile APIs that empower operators to execute actions within the
provider's system. These APIs operate as HTTPS listeners, monitoring incoming POST requests to
specific URLs, as delineated by the corresponding request mappings below.

All requests and responses are in JSON format

All request should contain header “Content-Type: application/json”
HTTP Methods : POST

Operator ID, secret key will be provided by provider for both production and test environments

The HTTPs service URL will be furnished by the provider for both production and test
environments. It takes the form of:

https://<API service domain>/api/opgateway/v1/op/<method>
or
https://<API service domain>/api/opgateway/v1/op/<path>/<method>
https://<API service domain>/api/opgateway/v1/op/<path>/<path>/<method>

The Integration HTTP Service is securely protected.

- Requests to the service should not be initiated from player browsers (end-users).
- IP addresses must be supplied to the provider for the purpose of whitelisting.


2.1 API Documentation
2.1.1 POST GetGameList
Request path: POST /GetGameList

Through this method, the operator gains the capability to retrieve a collection of accessible games from
the provider's system.

Request parameters
## Name Type Description Status
OperatorId String(20) Operator Id  Required
RequestDateTime String(50) UTC datetime (yyyy-MM-ddTHH:mm:ssZ)

**Using current UTC+0 datetime, this field is exclusively intended for
MD5 hashing and validation purposes. Please refrain from utilising it
for transactional records.
## Required
## Signature String(200
## )
MD5 (FunctionName + RequestDateTime + OperatorId + SecretKey)
(Please refer MD5 hashing function)
## Required
Lang String(50) Language code (ISO 639-1), default is “en-us” Optional
Currency String(50) Currency code, when not specified, default will be used Optional

Example of JSON request
## JSON
## {
"OperatorId": "DemoAccount",
"RequestDateTime": "2014-09-30T14:16:32Z",
"Signature": "8d3d050acf123op78a42328215872745"
## }

Response parameters
## Name Type Description
Status Integer Status code
Description String(50) Status description
ResponseDateTime String(50) UTC datetime (yyyy-MM-dd HH:mm:ss)

**Using current UTC+0 datetime, this field is exclusively intended for MD5 hashing
and validation purposes. Please refrain from utilising it for transactional records.
Game Array Game object array (Object field please refer following table)

continue.. Response parameters (Object Game)
## Name Type Description

GameCode String(50) Unique code of the game within the provider system
GameType Integer Game type
(Please refer Game Type)
GameName String(50) English game name / description
ImageUrl String(100
## )
Indicates the URL from which the English version of the game image should be
retrieved.
HasDemo Bool Indicates that this game is applicable for demo play

Example of JSON response
## JSON
## {
"Status": 200,
"Description": "Success",
"ResponseDateTime": "2016-09-01 09:41:37",
"Game": [
## {
"GameId": 35014,
"GameCode": "35014",
"GameName": "Wonders of Giza Pyramid",
"GameType": 1,
"ImageUrl": "https://<base-domain-url>/thumbs/web/35014.png",
"Method": "Slots",
"IsH5Support": true,
"Maintenance": "1|2|3|4|5|6",
"GameLobbyConfig": "1|1|1|1753401600",
"OtherName": [
## "zh-cn|奇迹之吉萨金字塔"
## ],
"HasDemo": true,
"Sequence": 1,
"GameEvent": [],
"GameProvideCode": "LGLive22",
"GameProvideName": "LG Live22",
"IsActive": true
## },
## {
"GameId": 35005,
"GameCode": "35005",
"GameName": "Slithering Riches",
"GameType": 1,
"ImageUrl": "https://<base-domain-url>/thumbs/web/35005.png",
"Method": "Slots",
"IsH5Support": true,

"Maintenance": "1|2|3|4|5|6",
"GameLobbyConfig": "0|1|1|1736812800",
"OtherName": [
## "zh-cn|蛇影富缘"
## ],
"HasDemo": true,
"Sequence": 1,
"GameEvent": [],
"GameProvideCode": "LGLive22",
"GameProvideName": "LG Live22",
"IsActive": true
## },
## ...
## ]
## }

2.1.2 POST GameLogin
Request path: POST /GameLogin

The operator invokes this method to obtain the game launch link.

Request parameters
## Name Type Description Status
OperatorId String(20) Operator Id  Required
RequestDateTime String(50) UTC datetime (yyyy-MM-ddTHH:mm:ssZ)

**Using current UTC+0 datetime, this field is exclusively intended for
MD5 hashing and validation purposes. Please refrain from utilising it
for transactional records.
## Required
Signature String(50) MD5 (FunctionName + RequestDateTime + OperatorId + SecretKey +
PlayerId)
(Please refer MD5 hashing function)
## Required
PlayerId String(50) Player’s Username from Operator (alphanumeric, normal symbol only &
no space allowed. (A-z, A-Z, 0-9, . _ $ - ?)
## Required
Ip String(50) Player Ip address, only support IPv4 Required
GameCode String(50) Unique Code of the game.  Required
Currency String(5) Eg: MYR: Malaysia Ringgit, SGD: Singapore Dollar
(Please refer Currency Code Table)
## Required
Lang String(5) Player language ISO code (Eg: en-us)
(Please refer Language Code Table)
## Optional
RedirectUrl String(100
## )
Back Lobby button Redirect Url Optional

AuthToken String(200
## )
The AuthToken serves to authenticate and validate a player's game
session. This token is added to callback requests made to the operator's
system, facilitating seamless execution on GetBalance, Bet and BuyIn
callback operations.
## Optional
DisplayName String(50) (Deprecated) Player display name Optional
PlayerBalance Decimal (Deprecated) Player current balance Optional
LaunchDemo Bool Indicate this game login should return demo launch URL. Default will be
false
## Optional

Example of JSON request
## JSON
## {
"OperatorId": "DemoAccount",
"RequestDateTime": "2014-09-30T14:16:32Z",
"Signature": "8d3d050acf123op78a42328215872745",
"PlayerId": "Player001",
"Ip": "192.168.2.2",
"GameCode": "10001",
"Currency": "MYR",
"Lang": "en-us",
"RedirectUrl": "https://<operator-lobby-url>.com",
"AuthToken":
"0rV2LzVUoLKCM3tbLvTkZW6ElA9jFkrhrm18ABouI27aG2gnEusTiMUfTLe0c1UxwWWBbkErK9qTKhCHxU
svCJUKjSywChcIz11Kx2vkdNwsdT1oU3PIUgZ8dyWQUQeiucw9E0odMvXpFYo3ub",
"LaunchDemo": false
## }

Response parameters
## Name Type Description
Status Integer Status code
Description String(50) Status description
ResponseDateTime String(50) UTC datetime (yyyy-MM-dd HH:mm:ss)

**Using current UTC+0 datetime, this field is exclusively intended for MD5 hashing
and validation purposes. Please refrain from utilising it for transactional records.
## Url String(200
## 0)
Game URL for player to launch the game


Example of JSON response
## JSON
## {
"Status": 200,

"Description": "Success",
"ResponseDateTime": "2016-09-01 09:41:37",
"Url": "https://<game-url>.com/slot/g/?p=2fht3VYQgXKMaUqxvomKPuz&rd=",
## }

2.1.3 GET LaunchGame
Request path: GET/LaunchGame

The operator invokes this method to obtain the game launch link.

Request parameters
## Name Type Description Status
OI String(20) Operator Id  Required
RD String(50) RequestDateTime field
UTC datetime (yyyy-MM-ddTHH:mm:ssZ)

**Using current UTC+0 datetime, this field is exclusively intended for
MD5 hashing and validation purposes. Please refrain from utilising it
for transactional records.
## Required
S String(50) Signature field
MD5 (FunctionName + RD + OI+ SecretKey + PI + IP + GC + C)
(Please refer MD5 hashing function)
## Required
PI String(50) Player’s Username from Operator (alphanumeric, normal symbol only &
no space allowed. (A-z, A-Z, 0-9, . _ $ - ?)
## Required
IP String(50) Player Ip address **IPv4 only  Required
GC String(50) GameCode field
Unique Code of the game.
## Required
C String(5) Currency field
Eg: MYR: Malaysia Ringgit, SGD: Singapore Dollar
(Please refer Currency Code Table)
## Required
L String(5) Player language ISO code (Eg: en-us)
(Please refer Language Code Table)
## Optional
RU String(100
## )
Back Lobby button Redirect Url Optional
AT String(200
## )
The AuthToken serves to authenticate and validate a player's game
session. This token is added to callback requests made to the operator's
system, facilitating seamless execution on GetBalance, Bet callback
operations.
## Optional

Example of JSON request
URL Parameter
https://<Operator-Gateway-Url>/?OI=DemoAccount&RD=2014-09-30T14:16:32&S=8d3d050acf123op78a42328215872745&PI=
Player001&IP=192.168.2.2&GC=10001&C=MYR&L=en-us&RU=https%3A%2F%2F%3Coperator-lobby-url%3E.com&AT=0rV2Lz

VUoLKCM3tbLvTkZW6ElA9jFkrhrm18ABouI27aG2gnEusTiMUfTLe0c1UxwWWBbkErK9qTKhCHxUsvCJUKjSywChcIz11Kx2vkd
NwsdT1oU3PIUgZ8dyWQUQeiucw9E0odMvXFYo3ub&LD=false

## Response:
HTTP status code 302 (Success)
-When the request is successful, the API responds with a
## 302 Found
status code, redirecting the client
to Game URL
-The
## Location
header in the response specifies the URL to which the client should redirect.

HTTP status code 200 (Error)
-Return HTML page with error status and description.
Response parameters
## Name Type Description
Status Integer Status code
Description String(50) Status description
ResponseDateTime String(50) UTC datetime (yyyy-MM-dd HH:mm:ss)

**Using current UTC+0 datetime, this field is exclusively intended for MD5 hashing
and validation purposes. Please refrain from utilising it for transactional records.

Example of HTML response
## HTML
## <html>
## <body>
<h1>Error</h1>
<div name="Status" value="900500">Status: <span>900500</span></div>
<div name="Description" value="Internal Server Error">Description: <span>Internal Server Error</span></div>
<div name="ResponseDateTime" value="2025-07-01 08:39:50">ResponseDateTime: <span>2025-07-01
## 08:39:50</span></div>
## </body>
## </html>


2.1.4 POST GetTransactionDetails
Request path: POST /GetTransactionDetails

The operator uses this method to obtain a report link that provides comprehensive transaction details by
utilising the game result id. Launching the URL in any supported browser will display the game's
transaction information.
**Subject to data availability may refer to real-time transaction policy 1.6 Data Retention Policy


Request parameters

## Name Type Description Status
OperatorId String(20) Operator Id  Required
RequestDateTime String(50) UTC datetime (yyyy-MM-ddTHH:mm:ssZ)

**Using current UTC+0 datetime, this field is exclusively intended for
MD5 hashing and validation purposes. Please refrain from utilising it
for transactional records.
## Required
Signature String(50) MD5 (FunctionName + RequestDateTime + OperatorId + SecretKey)
(Please refer MD5 hashing function)
## Required
TranId String(50) Transaction Id to view transaction details (ResultId, in GameResult, or
TranId in PullLog API)
**RoundId/Betid wont work
## Required

Example of JSON request
## JSON
## {
"OperatorId": "DemoAccount",
"RequestDateTime": "2014-09-30T14:16:32Z",
"Signature": "8d3d050acf123op78a42328215872745",
"TranId": "23250644"
## }

Response parameters
## Name Type Description
Status Integer Status code
Description String(50) Status description
ResponseDateTime String(50) UTC datetime (yyyy-MM-dd HH:mm:ss)

**Using current UTC+0 datetime, this field is exclusively intended for MD5 hashing
and validation purposes. Please refrain from utilising it for transactional records.
## Url String(200
## 0)
URL for open Transaction Details


Example of JSON response
## JSON
## {
"Status": 200,
"Description": "Success",
"ResponseDateTime": "2016-09-01 09:41:37",
"Url": "https://<game-transaction-url>.com/GameSeriesVXXX_Reporting/viewrounddetails",
## }

2.1.5 POST GetDaySummary
Request path: POST /GetDaySummary

This method is designed to furnish a summarised overview of daily transactions, categorised by currency.

Request parameters
## Name Type Description Status
OperatorId String(20) Operator Id  Required
RequestDateTime String(50) UTC datetime (yyyy-MM-ddTHH:mm:ssZ)

**Using current UTC+0 datetime, this field is exclusively intended for
MD5 hashing and validation purposes. Please refrain from utilising it
for transactional records.
## Required
Signature String(50) MD5 (FunctionName + RequestDateTime + OperatorId + SecretKey)
(Please refer MD5 hashing function)
## Required
Date DateTime UTC DateTime Required

Example of JSON request
## JSON
## {
"OperatorId": "DemoAccount",
"RequestDateTime": "2014-09-30T14:16:32Z",
"Signature": "8d3d050acf123op78a42328215872745",
"Date": "2023-08-18T00:00:00Z"
## }

Response parameters
## Name Type Description
Status Integer Status code
Description String(50) Status description
ResponseDateTime String(50) UTC datetime (yyyy-MM-dd HH:mm:ss)

**Using current UTC+0 datetime, this field is exclusively intended for MD5 hashing
and validation purposes. Please refrain from utilising it for transactional records.
Trans Array Transaction object array (Object field please refer following table)

continue.. Response parameters (Object Trans)
## Name Type Description
CurrencyCode String(5) Eg: MYR: Malaysia Ringgit, SGD: Singapore Dollar
(Please refer Currency Code Table)
Turnover Decimal Turnover amount (Eg: 12345678.1234)

ValidTurnover Decimal Valid turnover amount (Eg: 12345678.1234)
Payout Decimal Payout amount (Eg: 12345678.1234)
WinLose Decimal Winlose amount (Payout - Turnover), can be negative value (-ve)

Example of JSON response
## JSON
## {
"Status": 200,
"Description": "Success",
"ResponseDateTime": "2016-09-01 09:41:37",
"Trans": [
## {
"CurrencyCode": "MYR",
"Turnover": 1.00,
"ValidTurnover": 1.00,
"Payout": 1.80,
"WinLose": 0.80
## },
## {
"CurrencyCode": "THB",
"Turnover": 1.00,
"ValidTurnover": 1.00,
"Payout": 1.80,
"WinLose": 0.80
## },
## ...
## ]
## }
2.1.6 POST KickPlayer
Request path: POST /KickPlayer

Operators can utilise the KickPlayer method to temporarily kick players from continuing to play the game.
Please note that players are still able to login and continue playing the game in the next session.

Request parameters
## Name Type Description Status
OperatorId String(20) Operator Id  Required
RequestDateTime String(50) UTC datetime (yyyy-MM-ddTHH:mm:ssZ)

**Using current UTC+0 datetime, this field is exclusively intended for
MD5 hashing and validation purposes. Please refrain from utilising it
for transactional records.
## Required

Signature String(50) MD5 (FunctionName + RequestDateTime + OperatorId + SecretKey +
PlayerId)
(Please refer MD5 hashing function)
## Required
PlayerId String(50) Player Id in operator system Required

Example of JSON request
## JSON
## {
"OperatorId": "DemoAccount",
"RequestDateTime": "2014-09-30T14:16:32Z",
"Signature": "8d3d050acf123op78a42328215872745",
"PlayerId": "Player001"
## }

Response parameters
## Name Type Description
Status Integer Status code
(Please refer provider Error / Status Code Table)
Description String(50) Status description
ResponseDateTime String(50) UTC datetime (yyyy-MM-dd HH:mm:ss)

**Using current UTC+0 datetime, this field is exclusively intended for MD5 hashing
and validation purposes. Please refrain from utilising it for transactional records.

Example of JSON response
## JSON
## {
"Status": 200,
"Description": "Success",
"ResponseDateTime": "2016-09-01 09:41:37"
## }
2.1.7 POST GetUnfinishRound
Request path: POST /GetUnfinishRound

Operators can utilise the GetUnfinishedRound method to retrieve a list of unfinished rounds held by
players. Unfinished rounds are determined by the absence of a generated result for the particular round.

Request parameters
## Name Type Description Status
OperatorId String(20) Operator Id  Required

RequestDateTime String(50) UTC datetime (yyyy-MM-ddTHH:mm:ssZ)

**Using current UTC+0 datetime, this field is exclusively intended for
MD5 hashing and validation purposes. Please refrain from utilising it
for transactional records.
## Required
Signature String(50) MD5 (FunctionName + RequestDateTime + OperatorId + SecretKey +
PlayerId)
(Please refer MD5 hashing function)
## Required
PlayerId String(50) Player Id in operator system Required

Example of JSON request
## JSON
## {
"OperatorId": "DemoAccount",
"RequestDateTime": "2014-09-30T14:16:32Z",
"Signature": "8d3d050acf123op78a42328215872745",
"PlayerId": "Player001"
## }

Response parameters
## Name Type Description
Status Integer Status code
(Please refer provider Error / Status Code Table)
Description String(50) Status description
ResponseDateTime String(50) UTC datetime (yyyy-MM-dd HH:mm:ss)

**Using current UTC+0 datetime, this field is exclusively intended for MD5 hashing
and validation purposes. Please refrain from utilising it for transactional records.
Rounds Array List of unfinished rounds

continue.. Response parameters (Object Rounds)
## Name Type Description
RoundId String(50) Unique id for the round
GameId String(30) Unique id for the game
GameName String(50) Unique name for the game
Turnover Decimal Turnover Amount  (Eg: 12345678.1234)

Example of JSON response
## JSON
## {
"Status": 200,

"Description": "Success",
"ResponseDateTime": "2016-09-01 09:41:37",
"Rounds": [
## {
"RoundId": "100000000",
“GameId” : “10000”,
“GameName” : “GameName 000”,
“Turnover” : 1.00
## },
## {
"RoundId": "100000001",
“GameId” : “10001”,
“GameName” : “GameName 001”,
“Turnover” : 1.00
## },
## ],
## }
2.1.8 POST CancelRound
Request path: POST /CancelRound

Operators can use the CancelRound method to cancel rounds being held by players. Settled rounds
cannot be cancelled. (This action will cancel current round progress, refund player bet amount and end
the round, game will kick player if still in game. Relogin will start a new round)

In the scenario where players may hold rounds to obtain maximum benefits from certain promotions,
operators may integrate these methods to retrieve a list of these held rounds and take necessary actions.

**Subject to data availability may refer to real-time transaction policy 1.6 Data Retention Policy

**Please noted round only be able to cancel after 5 min from round id creation

Request parameters
## Name Type Description Status
OperatorId String(20) Operator Id  Required
RequestDateTime String(50) UTC datetime (yyyy-MM-ddTHH:mm:ssZ)

**Using current UTC+0 datetime, this field is exclusively intended for
MD5 hashing and validation purposes. Please refrain from utilising it
for transactional records.
## Required
Signature String(50) MD5 (FunctionName + RequestDateTime + OperatorId + SecretKey +
PlayerId)
(Please refer MD5 hashing function)
## Required
PlayerId String(50) Player Id in operator system Required
RoundId String(50) Unique id for the round Required

Example of JSON request

## JSON
## {
"OperatorId": "DemoAccount",
"RequestDateTime": "2014-09-30T14:16:32Z",
"Signature": "8d3d050acf123op78a42328215872745",
"PlayerId": "Player001",
"RoundId": "100000001"
## }

Response parameters
## Name Type Description
Status Integer Status code
(Please refer provider Error / Status Code Table)
Description String(50) Status description
ResponseDateTime String(50) UTC datetime (yyyy-MM-dd HH:mm:ss)

**Using current UTC+0 datetime, this field is exclusively intended for MD5 hashing
and validation purposes. Please refrain from utilising it for transactional records.

Example of JSON response
## JSON
## {
"Status": 200,
"Description": "Success",
"ResponseDateTime": "2016-09-01 09:41:37"
## }
2.1.9 POST SettleRound
Request path: POST /SettleRound

Operators can use the SettleRound method to settle rounds being held by players. Settled rounds will not
be processed. (This action will summarize current round progress as payout and end the round, game will
kick player if still in game. Relogin will start a new round)

In the scenario where players may hold rounds to obtain maximum benefits from certain promotions,
operators may integrate these methods to retrieve a list of these held rounds and take necessary actions.
Please noted we only accept Settle round when the round is still in progress and bet is accepted by
operator.

Request parameters
## Name Type Description Status
OperatorId String(20) Operator Id  Required

RequestDateTime String(50) UTC datetime (yyyy-MM-ddTHH:mm:ssZ)

**Using current UTC+0 datetime, this field is exclusively intended for
MD5 hashing and validation purposes. Please refrain from utilising it
for transactional records.
## Required
Signature String(50) MD5 (FunctionName + RequestDateTime + OperatorId + SecretKey +
PlayerId)
(Please refer MD5 hashing function)
## Required
PlayerId String(50) Player Id in operator system Required
RoundId String(50) Unique id for the round Required

Example of JSON request
## JSON
## {
"OperatorId": "DemoAccount",
"RequestDateTime": "2014-09-30T14:16:32Z",
"Signature": "8d3d050acf123op78a42328215872745",
"PlayerId": "Player001",
"RoundId": "100000001"
## }

Response parameters
## Name Type Description
Status Integer Status code
(Please refer provider Error / Status Code Table)
Description String(50) Status description
ResponseDateTime String(50) UTC datetime (yyyy-MM-dd HH:mm:ss)

**Using current UTC+0 datetime, this field is exclusively intended for MD5 hashing
and validation purposes. Please refrain from utilising it for transactional records.

Example of JSON response
## JSON
## {
"Status": 200,
"Description": "Success",
"ResponseDateTime": "2016-09-01 09:41:37"
## }


2.1.10 POST GetRoundDetails
Request path: POST /GetRoundDetails

Retrieve comprehensive information about a specific round. It provides detailed insights into various
aspects of a round, including the round has settled, has voided and the details of the round.
**Subject to data availability may refer to real-time transaction policy 1.6 Data Retention Policy


Request parameters
## Name Type Description Status
OperatorId String(20) Operator Id  Required
RequestDateTime String(50) UTC datetime (yyyy-MM-ddTHH:mm:ssZ)

**Using current UTC+0 datetime, this field is exclusively intended for
MD5 hashing and validation purposes. Please refrain from utilising it
for transactional records.
## Required
Signature String(50) MD5 (FunctionName + RequestDateTime + OperatorId + SecretKey)
(Please refer MD5 hashing function)
## Required
RoundId Long Unique id for the round Required
GameCode String(50) Unique Code of the game Required

Example of JSON request
## JSON
## {
"OperatorId": "DemoAccount",
"RequestDateTime": "2014-09-30T14:16:32Z",
"Signature": "8d3d050acf123op78a42328215872745",
"RoundId": "100000001",
“GameCode”: “10006”
## }

Response parameters
## Name Type Description
Status Integer Status code
(Please refer provider Error / Status Code Table)
Description String(50) Status description
ResponseDateTime String(50) UTC datetime (yyyy-MM-dd HH:mm:ss)

**Using current UTC+0 datetime, this field is exclusively intended for MD5 hashing
and validation purposes. Please refrain from utilising it for transactional records.
HasSettle Boolean Indicate the round is fully settled

HasVoid Boolean Indicate the round is voided
RoundDetails Object RoundDetails object (Object field please refer following table)

continue.. Response parameters (Object RoundDetails)
## Name Type Description
RoundId Long Unique id for the round
RoundTranDT String(50) DateTime for the round
ResultId Long Unique id for the result Noted: NULL if the round is unsettled or voided.
ResultTranDT String(50) DateTime for the result Noted: NULL if the round is unsettled or voided.
PlayerId String(50) PlayerId for the round
GameCode String(50) GameCode for the round
BetAmount Decimal Total BetAmount for the round
Payout Decimal Total Payout for the round Noted: NULL if the round is unsettled or voided.
ProviderTimeZone String Provider side Time Zone
ProviderRoundTran
## DT
DateTime DateTime for the round based on ProviderTimeZone
ProviderResultTran
## DT
DateTime DateTime for the result based on ProviderTimeZone

Example of JSON response
## JSON
## {
"HasSettle": true,
"HasVoid": false,
"RoundDetails": {
"RoundId": 109850647,
"RoundTranDT": "2023-11-17T04:07:20Z",
"ResultId": 109850648,
"ResultTranDT": "2023-11-17T04:07:20Z",
"PlayerId": "DemoGuest3",
"GameCode": "10014",
"BetAmount": -200,
"Payout": 0,
“ProviderTimeZone”: “Singapore Standard Time”,
“ProviderRoundTranDT”: "2023-11-17T12:07:20.000+08:00"
“ProviderResultTranDT”: "2023-11-17T12:07:20.000+08:00"
## },
"Status": 200,
"Description": "Success",

"ResponseDateTime": "2023-11-17 04:08:42"
## }
## 2.2 Demo Launch Game
There are two Different Methods to Launch a Demo Game from the Provider System.

Each of these methods offers distinct advantages and may be chosen based on the operator's strategy,
target audience, and technical capabilities. The choice of method can impact user engagement and
accessibility, so it's important for operators to consider their specific goals when implementing demo
game launch options.
2.2.1 GetGameList and GameLogin method

By utilising the "HasDemo" Field in the 2.1.1 GetGameList Method, operators can determine whether to
display a demo hyperlink or button that redirects players to the demo game.

To initiate a demo game session, operators can utilise the "LaunchDemo" Boolean Field in the 2.1.2
GameLogin Field to specify that this game login is for a demo session. It will trigger an "Invalid Game"
error if the game does not have a demo version available.
2.2.2 GET GameList
Request path: GET /demo/GameList?opId={opid}&lang={lang}

Operators can construct URLs based on the format described above and use them to retrieve supported
gamelist for demo play

Query Strings parameters
## Name Type Description Status
opId String(20) Operator Id  Required
Lang String(5) Player language ISO code (Eg: en-us)
(Please refer Language Code Table)
## Optional

Response please refer to 2.1.1 POST GetGameList response parameters.
2.2.3 GET LaunchGame
Request path: GET
/demo/LaunchGame?opId={opid}&currency={currency}&gameCode={gameCode}&redirectUrl={redirect
## Url}&lang={lang}

Operators can construct URLs based on the format described above and use them to redirect players
directly to demo games.

Query Strings parameters

## Name Type Description Status
opId String(20) Operator Id  Required
Currency String(5) Eg: MYR: Malaysia Ringgit, SGD: Singapore Dollar
(Please refer Currency Code Table)
## Required
GameCode String(50) Unique Code of the game.  Required
RedirectUrl String(100
## )
Back Lobby button Redirect Url Optional
Lang String(5) Player language ISO code (Eg: en-us)
(Please refer Language Code Table)
## Optional

2.3 Free Round Feature Integration API
The Free Round Feature API is a marketing tool used by operators to offer players free gameplay
sessions. Operators create and manage these sessions to attract and retain players, customise
promotions, and monitor their impact on the platform. This feature helps boost player engagement and
loyalty.
2.3.1 POST CreateFreeRound
Request path: POST /CreateFreeRound

Operators may utilise this method to grant players complimentary rounds in a variety of games.
**This API will only work if the player is exist in slotmaker system, please create Player beforehand if it is new player thru
2.1.2 POST GameLogin


Request parameters
## Name Type Description Status
OperatorId String(20) Operator Id  Required
RequestDateTime String(50) UTC datetime (yyyy-MM-ddTHH:mm:ssZ)

**Using current UTC+0 datetime, this field is exclusively intended for
MD5 hashing and validation purposes. Please refrain from utilising it
for transactional records.
## Required
Signature String(50) MD5 (FunctionName + RequestDateTime + OperatorId + SecretKey +
PlayerId)
(Please refer MD5 hashing function)
## Required
PlayerId String(50) Player Id in operator system Required
GameCode String(50) Unique code of the game, it indicates which game the player will access  Required
RoundType Integer Specifies the category or type of the round that is being created. Required
TotalRound Integer Specifies the total number of rounds that the player will receive as part of
the free round offer
## Required
BetValue Integer The value of a bet or wager associated with each round Required

## Name Type Description Status
LineBet Decimal The bet amount per line or payline Required
ReferenceId String Parameter that can be used to reference or link the free round creation
request to a specific transaction or event
## Required
MaxWinAmount Decimal Specifies the highest total winnings a player can achieve during their Free
Round session.
## Required
ExpiryInterval Integer Specifies the duration of time in days for which the Free Round session
remains valid and accessible to the player. (Noted: When this parameter is
not provided in the API request, the system will typically apply a default
value as part of its settings)
## Optional

Example of JSON request
## JSON
## {
"OperatorId": "DemoAccount",
"Signature": "8d3d050acf123op78a42328215872745",
"RequestDateTime": "2014-09-30T14:16:32Z",
"PlayerId": "Player001",
"GameCode": "10001",
"RoundType": 1,
"TotalRound": 10,
"BetValue": 1,
"LineBet": 0.1,
"ReferenceId": "test",
"MaxWinAmount": 100.00,
"ExpiryInterval": 1
## }

Response parameters
## Name Type Description
Status Integer Status code
Description String(50) Status description
ResponseDateTime String(50) UTC datetime (yyyy-MM-dd HH:mm:ss)

**Using current UTC+0 datetime, this field is exclusively intended for MD5 hashing
and validation purposes. Please refrain from utilising it for transactional records.
FreeRoundId Long Identifier associated with the created free round, allowing the operator to reference and
manage it.
ExpiryTimeStamp Long Indicates the Unix timestamp when the free round will expire or become unavailable

Example of JSON response
## JSON

## {
"Status": 200,
"Description": "Success",
"ResponseDateTime": "2016-09-01 09:41:37",
"FreeRoundId": 123,
"ExpiryTimeStamp": 1694023495
## }
2.3.2 POST CancelFreeRound
Request path: POST /CancelFreeRound

Method that enables operators to revoke or nullify a previously granted free round.

Request parameters
## Name Type Description Status
OperatorId String(20) Operator Id  Required
RequestDateTime String(50) UTC datetime (yyyy-MM-ddTHH:mm:ssZ)

**Using current UTC+0 datetime, this field is exclusively intended for
MD5 hashing and validation purposes. Please refrain from utilising it
for transactional records.
## Required
Signature String(50) MD5 (FunctionName + RequestDateTime + OperatorId + SecretKey +
PlayerId)
(Please refer MD5 hashing function)
## Required
PlayerId String(50) Player Id in operator system Required
FreeRoundId Long Identifier associated with the created free round, allowing the operator to
reference and manage it.
## Required

Example of JSON request
## JSON
## {
"OperatorId": "DemoAccount",
"Signature": "8d3d050acf123op78a42328215872745",
"RequestDateTime": "2014-09-30T14:16:32Z",
"PlayerId": "Player001",
"FreeRoundId": 123
## }

Response parameters
## Name Type Description
Status Integer Status code
Description String(50) Status description

ResponseDateTime String(50) UTC datetime (yyyy-MM-dd HH:mm:ss)

**Using current UTC+0 datetime, this field is exclusively intended for MD5 hashing
and validation purposes. Please refrain from utilising it for transactional records.

Example of JSON response
## JSON
## {
"Status": 200,
"Description": "Success",
"ResponseDateTime": "2016-09-01 09:41:37"
## }
2.3.3 POST GetFreeRoundInfoByPlayer
Request path: POST /GetFreeRoundInfoByPlayer

This method allows operators to access detailed information about player's free rounds, aiding in better
player management and engagement.

Request parameters
## Name Type Description Status
OperatorId String(20) Operator Id  Required
RequestDateTime String(50) UTC datetime (yyyy-MM-ddTHH:mm:ssZ)

**Using current UTC+0 datetime, this field is exclusively intended for
MD5 hashing and validation purposes. Please refrain from utilising it
for transactional records.
## Required
Signature String(50) MD5 (FunctionName + RequestDateTime + OperatorId + SecretKey +
PlayerId)
(Please refer MD5 hashing function)
## Required
PlayerId String(50) Player Id in operator system Required

Example of JSON request
## JSON
## {
"OperatorId": "DemoAccount",
"Signature": "8d3d050acf123op78a42328215872745",
"RequestDateTime": "2014-09-30T14:16:32Z",
"PlayerId": "Player001"
## }

Response parameters
## Name Type Description

Status Integer Status code
Description String(50) Status description
ResponseDateTime String(50) UTC datetime (yyyy-MM-dd HH:mm:ss)

**Using current UTC+0 datetime, this field is exclusively intended for MD5 hashing
and validation purposes. Please refrain from utilising it for transactional records.
FreeRoundInfos Array FreeRoundInfo object array (Object field please refer following table)

continue.. Response parameters (Object FreeRoundInfos)
## Name Type Description
FreeRoundId Long Identifier associated with the created free round, allowing the operator to reference and
manage it.
GameCode String(50) Unique code of the game, it indicates which game the player will access
ExpiryTimeStamp Long Indicates the Unix timestamp when the free round will expire or become unavailable
RoundType Integer Specifies the category or type of the round that is being created.
BetValue Integer The value of a bet or wager associated with each round
LineBet Decimal The bet amount per line or payline
CurrentRound Integer Specifies the current round within the free round gameplay, It indicates how many
rounds have been played.
TotalRound Integer Specifies the total number of rounds that the player will receive as part of the free round
offer
TotalWin Decimal Represents the cumulative winnings amount by the player using this free round.
Status Integer Status of the free round.

## Register = 0
OnGoing = 1
## Completed = 2
## Claimed = 3
## Cancelled = 400
## Expired = 500

Example of JSON response
## JSON
## {
"FreeRoundInfos": [
## {
"FreeRoundId": 123,
"GameCode": "10001",
"ExpiryTimeStamp": 1694023495,
"RoundType": 1,
"BetValue": 1,
"LineBet": 0.1,

"CurrentRound": 0,
"TotalRound": 10,
"TotalWin": 0,
"Status": 0
## }
## ],
"Status": 200,
"Description": "Success",
"ResponseDateTime": "2016-09-01 09:41:37"
## }
2.3.4 POST GetFreeRoundGames
Request path: POST /GetFreeRoundGames

Retrieve a list of game information that are eligible for free rounds.

Request parameters
## Name Type Description Status
OperatorId String(20) Operator Id  Required
RequestDateTime String(50) UTC datetime (yyyy-MM-ddTHH:mm:ssZ)

**Using current UTC+0 datetime, this field is exclusively intended for
MD5 hashing and validation purposes. Please refrain from utilising it
for transactional records.
## Required
Signature String(50) MD5 (FunctionName + RequestDateTime + OperatorId + SecretKey)
(Please refer MD5 hashing function)
## Required

Example of JSON request
## JSON
## {
"OperatorId": "DemoAccount",
"Signature": "8d3d050acf123op78a42328215872745",
"RequestDateTime": "2014-09-30T14:16:32Z",
## }

Response parameters
## Name Type Description
Status Integer Status code
Description String(50) Status description
ResponseDateTime String(50) UTC datetime (yyyy-MM-dd HH:mm:ss)

**Using current UTC+0 datetime, this field is exclusively intended for MD5 hashing
and validation purposes. Please refrain from utilising it for transactional records.

Games Array Game object array (Object field please refer following table)

continue.. Response parameters (Object Games)
## Name Type Description
GameCode String(50) Unique code of the game
GameName String(50) Name of the game
TotalLine Integer Total line of the game
AvailableRoundType Array AvailableRoundType object array (Object field please refer following table)
AvailableBetValue Array of Integer Available bet values for the game
AvailableLineBet Array AvailableLineBet object array (Object field please refer following table)
MaxSpinCountCap Integer Maximum Spin Count Cap for the game
MaxWinCapMultiplier Integer Maximum Winning Cap Multiplier for the game

continue.. Response parameters (Object AvailableRoundType)
## Name Type Description
RoundType Integer Identifier for the round type
RoundTypeName String(50) Label for the round type, providing a description of what each type represents

continue.. Response parameters (Object AvailableLineBet)
## Name Type Description
## Currency String(50) Currency Code
LineBets Array of Decimal Available line bet for the currency

Example of JSON response
## JSON
## {
"Games": [
## {
"GameCode": "10050",
"GameName": "Blessing of Tu",
"TotalLine": 40,
"AvailableRoundType": [
## {
"RoundType": 1,
"RoundTypeName": "Normal"
## }
## ],
"AvailableBetValue": [

## 1
## ],
"AvailableLineBet": [
## {
"Currency": "MYR",
"LineBets": [
## 0.005,
## 0.01,
## 0.02,
## 0.03,
## 0.04,
## 0.05
## ]
## }
## ],
"MaxSpinCountCap": 100,
"MaxWinCapMultiplier": 1000
## }
## ],
"Status": 200,
"Description": "Success",
"ResponseDateTime": "2023-09-19 12:27:17"
## }

2.3.5 POST GetFreeRoundDetails
Request path: POST /GetFreeRoundDetails

Retrieve all transaction information for a specific free round.

Request parameters
## Name Type Description Status
OperatorId String(20) Operator Id  Required
RequestDateTime String(50) UTC datetime (yyyy-MM-ddTHH:mm:ssZ)

**Using current UTC+0 datetime, this field is exclusively intended for
MD5 hashing and validation purposes. Please refrain from utilising it
for transactional records.
## Required
Signature String(50) MD5 (FunctionName + RequestDateTime + OperatorId + SecretKey +
PlayerId)
(Please refer MD5 hashing function)
## Required
PlayerId String(50) Player Id in operator system Required
FreeRoundId Long Free Round Id Required


Example of JSON request
## JSON
## {
"OperatorId": "DemoAccount",
"Signature": "8d3d050acf123op78a42328215872745",
"RequestDateTime": "2014-09-30T14:16:32Z",
"PlayerId": "Player001",
"FreeRoundId": 123
## }

Response parameters
## Name Type Description
Status Integer Status code
Description String(50) Status description
ResponseDateTime String(50) UTC datetime (yyyy-MM-dd HH:mm:ss)

**Using current UTC+0 datetime, this field is exclusively intended for MD5 hashing
and validation purposes. Please refrain from utilising it for transactional records.
Trans Array FreeRoundDetailsInfo object array (Object field please refer following table)
IsMaxWin Bool To indicate if the round has reached max win
MaxWinAmount Decimal Nullable, max win amount for this free round

continue.. Response parameters (Object FreeRoundDetailsInfo)
## Name Type Description
TranDateTime DateTime  UTC DateTime (yyyy-MM-ddTHH:mm:ssZ) of the free round transaction
GameId Integer Game Id of the game played for this free round
GameName String Name of the game played for this free round
Turnover Decimal Turnover amount (Eg: 12345678.1234)
Payout Decimal Payout amount (Eg: 12345678.1234)

**Can be 0 (‘ZERO’) value if the round doesn’t generate payout
WinLose Decimal WinLose amount (ValidTurnover - Payout)
RoundType String Type of the Round played (Normal or Buy Free Spin)
TranId Long Transaction Id of the Free Round detail
ProviderTimeZone String Provider side Time Zone
ProviderTranDt DateTime Date time of the free round transaction based on ProviderTimeZone

Example of JSON response

## JSON
## {
"Trans": [
## {
"TranDateTime": "2023-09-19T14:25:59.45Z",
"GameId": 10050,
"GameName": “Game Name”,
"Turnover": 40,
"Payout": 0,
"WinLose": 40,
"RoundType": “Normal”,
"TranId": 1223,
"ProviderTimeZone":"Singapore Standard Time",
"ProviderTranDt":""2023-09-19T22:25:59.451+08:00"
## }
## ],
"IsMaxWin": true,
"MaxWinAmount": 50,
"Status": 200,
"Description": "Success",
"ResponseDateTime": "2023-09-30 09:41:37"
## }
2.3.6 POST GetFreeRoundInfoByOperator
Request path: POST /GetFreeRoundInfoByOperator

This method allows operators to access detailed information about operator's free rounds, aiding in better
player management and engagement.

Request parameters
## Name Type Description Status
OperatorId String(20) Operator Id  Required
RequestDateTime String(50) UTC datetime (yyyy-MM-ddTHH:mm:ssZ)

**Using current UTC+0 datetime, this field is exclusively intended for
MD5 hashing and validation purposes. Please refrain from utilising it
for transactional records.
## Required
Signature String(50) MD5 (FunctionName + RequestDateTime + OperatorId + SecretKey)
(Please refer MD5 hashing function)
## Required
Page Integer Page number (Each Page content 50 record max) Required

Example of JSON request
## JSON

## {
"OperatorId": "DemoAccount",
"Signature": "116bfb2145a461563a3ea04c9996f770",
"RequestDateTime": "2024-10-07T17:56:00Z",
“Page”:1
## }

Response parameters
## Name Type Description
Status Integer Status code
Description String(50) Status description
ResponseDateTime String(50) UTC datetime (yyyy-MM-dd HH:mm:ss)

**Using current UTC+0 datetime, this field is exclusively intended for MD5 hashing
and validation purposes. Please refrain from utilising it for transactional records.
FreeRoundInfos Array FreeRoundInfo object array (Object field please refer following table)
TotalPage Integer Total page number

continue.. Response parameters (Object FreeRoundInfos)
## Name Type Description
FreeRoundId Long Identifier associated with the created free round, allowing the operator to reference and
manage it.
GameCode String(50) Unique code of the game, it indicates which game the player will access
ExpiryTimeStamp Long Indicates the Unix timestamp when the free round will expire or become unavailable
RoundType Integer Specifies the category or type of the round that is being created.
BetValue Integer The value of a bet or wager associated with each round
LineBet Decimal The bet amount per line or payline
CurrentRound Integer Specifies the current round within the free round gameplay, It indicates how many
rounds have been played.
TotalRound Integer Specifies the total number of rounds that the player will receive as part of the free round
offer
TotalWin Decimal Represents the cumulative winnings amount by the player using this free round.
Status Integer Status of the free round.

## Register = 0
OnGoing = 1
## Expired = 500
PlayerId String(50) Player Id in operator system

Example of JSON response

## JSON
## {
"FreeRoundInfos": [
## {
"FreeRoundId": 123,
"GameCode": "10001",
"ExpiryTimeStamp": 1694023495,
"RoundType": 1,
"BetValue": 1,
"LineBet": 0.1,
"CurrentRound": 0,
"TotalRound": 10,
"TotalWin": 0,
"Status": 0,
“PlayerId”: "Player001"
## }
## ],
"Status": 200,
"Description": "Success",
"ResponseDateTime": "2016-09-01 09:41:37",
“TotalPage”:3
## }



- Seamless Wallet Integration API
This collection encompasses a suite of seamless APIs designed for the provider's gaming platform to
establish connections with players' wallets.

All requests and responses are in JSON format

All request will contain header “Content-Type: application/json”
HTTP Methods : POST

Operator ID, secret key will be provided by provider for both production and test environments

The HTTPs service URL should be provided by the Operator for the production and test
environments.

The Integration HTTP Service is securely protected.

- Service requests originate exclusively from provider servers via multiple proxied machines.
- IP addresses will be furnished for whitelisting purposes.

Please whitelist these IP for according to the specific environment to allow provider outbound API
request to reach operator’s system

## UAT
## -175.41.155.108

## PROD
## -18.142.217.186
## -3.0.144.240
## -13.228.208.147

## 3.1 Game Opening Method
The operator can obtain a valid game launch URL through the Integration API 2.2 GameLogin method.
This launch URL is applicable for opening the game in any supported web browser or webview.


3.2 API Documentation
3.2.1 POST GetBalance
Request path: POST /GetBalance

This function facilitates the retrieval of a player's current balance.

Request parameters
## Name Type Description
OperatorId String(20) Operator Id
RequestDateTime String(50) UTC datetime (yyyy-MM-ddTHH:mm:ssZ)

**Using current UTC+0 datetime, this field is exclusively intended for MD5
hashing and validation purposes. Please refrain from utilising it for transactional
records.
Signature String(50) MD5 (FunctionName + RequestDateTime + OperatorId + SecretKey + PlayerId)
(Please refer MD5 hashing function)
PlayerId String(50) Player Id in operator system
Currency String(5) Eg: MYR: Malaysia Ringgit, SGD: Singapore Dollar
(Please refer Currency Code Table)
AuthToken String(200
## )
The AuthToken serves to authenticate and validate a player's game session. This token
is added when the operator initiates gamelogin with AuthToken.

Example of JSON request
## JSON
## {
"OperatorId": "DemoAccount",
"RequestDateTime": "2014-09-30T14:16:32Z",
"Signature": "8d3d050acf123op78a42328215872745",
"PlayerId": "Player001"
"Currency": "MYR",
"AuthToken":
"0rV2LzVUoLKCM3tbLvTkZW6ElA9jFkrhrm18ABouI27aG2gnEusTiMUfTLe0c1UxwWWBbkErK9qTKhCHxU
svCJUKjSywChcIz11Kx2vkdNwsdT1oU3PIUgZ8dyWQUQeiucw9E0odMvXpFYo3ub"
## }

Response parameters
## Name Type Description
Status Integer Status code
(Please refer operator Error / Status Code Table)
Description String(50) Status description
ResponseDateTime String(50) UTC datetime (yyyy-MM-dd HH:mm:ss)


**Using current UTC+0 datetime, this field is exclusively intended for MD5 hashing
and validation purposes. Please refrain from utilising it for transactional records.
Balance Decimal Player’s available balance (eg: 1233.5000)

Example of JSON response
## JSON
## {
"Status": 200,
"Description": "Success",
"ResponseDateTime": "2016-09-01 09:41:37"
## }
3.2.2 POST Bet
Request path: POST /Bet

Checks if the player has enough funds and subtracts money from the player's balance. Returns the value
of updated balance.

Important: The call is idempotent, i.e. sending a bet again with the same BetId only creates one transaction. Operator’s
system must not process the same transaction which has the same BetId twice.

Request parameters
## Name Type Description
OperatorId String(20) Operator Id
RequestDateTime String(50) UTC datetime (yyyy-MM-ddTHH:mm:ssZ)

**Using current UTC+0 datetime, this field is exclusively intended for MD5
hashing and validation purposes. Please refrain from utilising it for transactional
records.
Signature String(50) MD5 (FunctionName + BetId + RequestDateTime + OperatorId + SecretKey + PlayerId)
(Please refer MD5 hashing function)
PlayerId String(50) Player Id in operator system
Currency String(5) Eg: MYR: Malaysia Ringgit, SGD: Singapore Dollar
(Please refer Currency Code Table)
RoundId Long Unique round id of the game round, multiple players may share the same round id
BetId Long Unique bet transaction id of the game round on provider system

**Use this value to ensure transaction uniqueness
GameCode String(50) Unique Code of the game.
GameType String(50) Game Type in string. (Eg: Slots / Arcade)

(Please refer Game Type)
BetAmount Decimal Bet amount (Eg: 12345678.1234)

**Use this value to update player balance
ExchangeRate Decimal Exchange rate (Eg: 1.0000)
TranDateTime DateTime Actual Transaction UTC DateTime (yyyy-MM-dd HH:mm:ss) on Provider system.

**This is the actual date and time when the bets were placed, verified within the
provider's game system.
AuthToken String(200
## )
The AuthToken serves to authenticate and validate a player's game session. This token
is added when the operator initiates gamelogin with AuthToken.
ProviderTimeZone String Provider side Time Zone
ProviderTranDt DateTime Actual Transaction DateTime based on ProviderTimeZone

Example of JSON request
## JSON
## {
"OperatorId": "DemoAccount",
"RequestDateTime": "2014-09-30T14:16:32Z",
"Signature": "8d3d050acf123op78a42328215872745",
"PlayerId": "Player001"
"Currency": "MYR",
"RoundId": 438664,
"BetId": 438665,
"BetAmount": 0.2000,
"ExchangeRate": 1.0000,
"GameCode": "10000",
"GameType": “Slots”,
"TranDateTime": "2014-09-30 14:16:32",
"AuthToken":
"0rV2LzVUoLKCM3tbLvTkZW6ElA9jFkrhrm18ABouI27aG2gnEusTiMUfTLe0c1UxwWWBbkErK9qTKhCHxU
svCJUKjSywChcIz11Kx2vkdNwsdT1oU3PIUgZ8dyWQUQeiucw9E0odMvXpFYo3ub",
"ProviderTimeZone": "Singapore Standard Time",
"ProviderTranDt": "2014-09-30T22:16:32.000+08:00"
## }

Response parameters
## Name Type Description
Status Integer Status code
(Please refer operator Error / Status Code Table)
Description String(50) Status description
ResponseDateTime String(50) UTC datetime (yyyy-MM-dd HH:mm:ss)


**Using current UTC+0 datetime, this field is exclusively intended for MD5 hashing
and validation purposes. Please refrain from utilising it for transactional records.
OldBalance Decimal Player’s balance before deduct bet amount (eg: 1233.5000)
NewBalance Decimal Player’s balance after deducted bet amount (eg: 1233.5000)

Example of JSON response
## JSON
## {
"Status": 200,
"Description": "Success",
"ResponseDateTime": "2016-09-01 09:41:37",
"OldBalance": 100.0000,
"NewBalance": 98.0000
## }
3.2.3 POST GameResult
Request path: POST /GameResult

Completion of a game round, the winning amount is added to the player's balance, reflecting the
conclusion of gameplay. The updated balance value is returned.

Important: The call is idempotent, i.e. sending the result again with the same ResultId creates only one
transaction.Operator’s system must not process the same transaction which has the same ResultId twice.

Request parameters
## Name Type Description
OperatorId String(20) Operator Id
RequestDateTime String(50) UTC datetime (yyyy-MM-ddTHH:mm:ssZ)

**Using current UTC+0 datetime, this field is exclusively intended for MD5 hashing
and validation purposes. Please refrain from utilising it for transactional records.
Signature String(50) MD5 (FunctionName + ResultId + RequestDateTime + OperatorId + SecretKey +
PlayerId)
(Please refer MD5 hashing function)
PlayerId String(50) Player Id in operator system
Currency String(5) Eg: MYR: Malaysia Ringgit, SGD: Singapore Dollar
(Please refer Currency Code Table)
ResultId Long Unique result transaction id of the game round on provider system

**Use this value to ensure transaction uniqueness
**Apply this TranId in the 2.1.3 GetTransactionDetails method to access a
comprehensive view of the game's transaction details.

BetId Long Unique bet transaction id of the game round on provider system
RoundId Long Unique round id of the game round, multiple players may share the same round id
GameCode String(50) Unique Code of the game.
GameType String(50) Game Type in string. (Eg: Slots / Arcade)
(Please refer Game Type)
GameName String(50) English game name / description
ResultType Integer Game Result Type:
(Please refer Game Result Type)
BetAmount Decimal Bet amount (Eg: 12345678.1234)
ValidBetAmount Decimal Valid Bet amount (Eg: 12345678.1234)
Payout Decimal Payout (Eg: 12345678.1234)

**Can be 0 (‘ZERO’) value if the round doesn’t generate payout
**Use this value to update player balance
WinLose Decimal Winlose amount (Payout - Turnover)

**Can be negative value (-ve)
ExchangeRate Decimal Exchange rate (Eg: 1.0000)
TranDateTime DateTime Actual Transaction UTC DateTime (yyyy-MM-dd HH:mm:ss) on Provider system.

**This is the actual date and time when the bets were placed, verified within the
provider's game system.
ProviderTimeZone String Provider side Time Zone
ProviderTranDt DateTime Actual Transaction DateTime based on ProviderTimeZone
RoundType Integer Round Type:
(Please refer RoundType)

Example of JSON request
## JSON
## {
"OperatorId": "DemoAccount",
"RequestDateTime": "2014-09-30T14:16:32Z",
"Signature": "8d3d050acf123op78a42328215872745",
"PlayerId": "Player001"
"Currency": "MYR",
"ResultId": 438666,
"BetId": 438665,
"RoundId": 438664,
"GameCode": "10000",
"GameType": “Slots”,
"GameName": "Game 001",
"ResultType": 0,

"BetAmount": 0.2000,
"ValidBetAmount": 0.2000,
"Payout": 0.0000,
"WinLose": -0.2000,
"ExchangeRate": 1.0000,
"TranDateTime": "2014-09-30 14:16:32",
"ProviderTimeZone": "Singapore Standard Time",
"ProviderTranDt": "2014-09-30T22:16:32.000+08:00",
"RoundType": 0
## }

Response parameters
## Name Type Description
Status Integer Status code
(Please refer operator Error / Status Code Table)
Description String(50) Status description
ResponseDateTime String(50) UTC datetime (yyyy-MM-dd HH:mm:ss)

**Using current UTC+0 datetime, this field is exclusively intended for MD5 hashing
and validation purposes. Please refrain from utilising it for transactional records.
OldBalance Decimal Player’s balance before add payout (eg: 1233.5000)
NewBalance Decimal Player’s balance after added payout (eg: 1233.5000)

Example of JSON response
## JSON
## {
"Status": 200,
"Description": "Success",
"ResponseDateTime": "2016-09-01 09:41:37",
"OldBalance": 100.0000,
"NewBalance": 102.0000
## }
3.2.4 POST Rollback
Request path: POST /Rollback

In the event of a bet cancellation due to an unfinished game, this method refunds the player's balance.

Important: The call is idempotent, i.e. sending the rollback again with the same BetId creates only one
transaction.Operator’s system must not process the same rollback transaction which has the same BetId twice.


Request parameters
## Name Type Description
OperatorId String(20) Operator Id
RequestDateTime String(50) UTC datetime (yyyy-MM-ddTHH:mm:ssZ)

**Using current UTC+0 datetime, this field is exclusively intended for MD5
hashing and validation purposes. Please refrain from utilising it for transactional
records.
Signature String(50) MD5 (FunctionName + BetId + RequestDateTime + OperatorId + SecretKey + PlayerId)
(Please refer MD5 hashing function)
PlayerId String(50) Player Id in operator system
Currency String(5) Eg: MYR: Malaysia Ringgit, SGD: Singapore Dollar
(Please refer Currency Code Table)
RoundId Long Unique round id of the game round, multiple players may share the same round id
BetId Long

Unique bet transaction id of the game round on provider system

**Use this value to ensure transaction uniqueness
GameCode String(50) Unique Code of the game.
GameType String(50) Game Type in string. (Eg: Slots / Arcade)
(Please refer Game Type)
BetAmount Decimal Bet amount (Eg: 12345678.1234)

**Use this value to update player balance
ExchangeRate Decimal Exchange rate (Eg: 1.0000)
TranDateTime DateTime Actual Transaction UTC DateTime (yyyy-MM-dd HH:mm:ss) on Provider system.

**This is the actual date and time when the bets were placed, verified within the
provider's game system.
RollbackType Integer Rollback Type
(Please refer Rollback Type)
ProviderTimeZone String Provider side Time Zone
ProviderTranDt DateTime Actual Transaction DateTime based on ProviderTimeZone

Example of JSON request
## JSON
## {
"OperatorId": "DemoAccount",
"RequestDateTime": "2014-09-30T14:16:32Z",
"Signature": "8d3d050acf123op78a42328215872745",
"PlayerId": "Player001"
"Currency": "MYR",
"RoundId": 438664,
"BetId": 438665,

"BetAmount": 0.2000,
"ExchangeRate": 1.0000,
"GameCode": "10000",
"GameType": “Slots”,
"TranDateTime": "2014-09-30 14:16:32",
"RollbackType": 1,
"ProviderTimeZone": "Singapore Standard Time",
"ProviderTranDt": "2014-09-30T22:16:32.000+08:00"
## }

Response parameters
## Name Type Description
Status Integer Status code
(Please refer operator Error / Status Code Table)
Description String(50) Status description
ResponseDateTime String(50) UTC datetime (yyyy-MM-dd HH:mm:ss)

**Using current UTC+0 datetime, this field is exclusively intended for MD5 hashing
and validation purposes. Please refrain from utilising it for transactional records.
OldBalance Decimal Player’s balance before deduct bet amount (eg: 1233.5000)
NewBalance Decimal Player’s balance after deducted bet amount (eg: 1233.5000)

Example of JSON response
## JSON
## {
"Status": 200,
"Description": "Success",
"ResponseDateTime": "2016-09-01 09:41:37",
"OldBalance": 100.0000,
"NewBalance": 98.0000
## }
3.2.5 POST CashBonus
Request path: POST /CashBonus

Implemented in provider campaigns, tournaments, and cash drops, this method informs the operator
about a player's bonus winnings, leading to an increase in the balance.

Important: The call is idempotent, i.e. sending the bonus again with the same TranId creates only one
transaction.Operator’s system must not process the same transaction which has the same TranId twice.


Request parameters
## Name Type Description
OperatorId String(20) Operator Id
RequestDateTime String(50) UTC datetime (yyyy-MM-ddTHH:mm:ssZ)

**Using current UTC+0 datetime, this field is exclusively intended for MD5
hashing and validation purposes. Please refrain from utilising it for transactional
records.
Signature String(50) MD5 (FunctionName + TranId + RequestDateTime + OperatorId + SecretKey +
PlayerId)
(Please refer MD5 hashing function)
PlayerId String(50) Player Id in operator system
Currency String(5) Eg: MYR: Malaysia Ringgit, SGD: Singapore Dollar
(Please refer Currency Code Table)
TranId String(25) Unique transaction id of the bonus on provider system

**Use this value to ensure transaction uniqueness
BonusId String(50) Unique bonus codes represent different bonus types.
BonusName String(50) Cash bonus Reward Name
BonusType Integer Cash bonus Reward Type
(Please refer Bonus Type)
Payout Decimal Payout amount (Eg: 12345678.1234)

**Use this value to update player balance
ExchangeRate Decimal Exchange rate (Eg: 1.0000)
TranDateTime DateTime Actual Transaction UTC DateTime (yyyy-MM-dd HH:mm:ss) on Provider system.

**This is the actual date and time when the bets were placed, verified within the
provider's game system.
## Result String(100
## )
Cash bonus result in string
(Please refer Result)
ProviderTimeZone String Provider side Time Zone
ProviderTranDt DateTime Actual Transaction DateTime based on ProviderTimeZone

Example of JSON request
## JSON
## {
"OperatorId": "DemoAccount",
"RequestDateTime": "2014-09-30T14:16:32Z",
"Signature": "8d3d050acf123op78a42328215872745",
"PlayerId": "Player001"
"Currency": "MYR",
"TranId": "438665",

"BonusId": "TNN2023",
"BonusName": “Tournament 2023”,
“BonusType”: 1,
"Payout": 200.0000,
"ExchangeRate": 1.0000,
"TranDateTime": "2014-09-30 14:16:32",
"Result": “1st place”,
"ProviderTimeZone": "Singapore Standard Time",
"ProviderTranDt": "2014-09-30T22:16:32.000+08:00"
## }

Response parameters
## Name Type Description
Status Integer Status code
(Please refer operator Error / Status Code Table)
Description String(50) Status description
ResponseDateTime String(50) UTC datetime (yyyy-MM-dd HH:mm:ss)

**Using current UTC+0 datetime, this field is exclusively intended for MD5 hashing
and validation purposes. Please refrain from utilising it for transactional records.
OldBalance Decimal Player’s balance before add payout amount (eg: 1233.5000)
NewBalance Decimal Player’s balance after added payout amount (eg: 1233.5000)

Example of JSON response
## JSON
## {
"Status": 200,
"Description": "Success",
"ResponseDateTime": "2016-09-01 09:41:37",
"OldBalance": 100.0000,
"NewBalance": 200.0000
## }


3.2.7 POST BetNSettle
Request path: POST /BetNSettle

Bet and settle of a game round, the winning amount is added to the player's balance, reflecting the
conclusion of gameplay. The updated balance value is returned.

Important: The call is idempotent, i.e. sending the BetNsettle again with the same Betid creates only one
transaction.Operator’s system must not process the same transaction which has the same Betid twice.

Request parameters
## Name Type Description
OperatorId String(20) Operator Id
RequestDateTime String(50) UTC datetime (yyyy-MM-ddTHH:mm:ssZ)

**Using current UTC+0 datetime, this field is exclusively intended for MD5 hashing
and validation purposes. Please refrain from utilising it for transactional records.
Signature String(50) MD5 (FunctionName + ResultId + RequestDateTime + OperatorId + SecretKey +
PlayerId)
(Please refer MD5 hashing function)
PlayerId String(50) Player Id in operator system
Currency String(5) Eg: MYR: Malaysia Ringgit, SGD: Singapore Dollar
(Please refer Currency Code Table)
ResultId Long Unique result transaction id of the game round on provider system

**Use this value to ensure transaction uniqueness
**Apply this TranId in the 2.1.3 GetTransactionDetails method to access a
comprehensive view of the game's transaction details.
BetId Long Unique bet transaction id of the game round on provider system
RoundId Long Unique round id of the game round, multiple players may share the same round id
GameCode String(50) Unique Code of the game.
GameType String(50) Game Type in string. (Eg: Slots / Arcade)
(Please refer Game Type)
GameName String(50) English game name / description
ResultType Integer Game Result Type:
(Please refer Game Result Type)
BetAmount Decimal Bet amount (Eg: 12345678.1234)
ValidBetAmount Decimal Valid Bet amount (Eg: 12345678.1234)
Payout Decimal Payout (Eg: 12345678.1234)

**Can be 0 (‘ZERO’) value if the round doesn’t generate payout
**Use this value to update player balance

WinLose Decimal Winlose amount (Payout - Turnover)

**Can be negative value (-ve)
ExchangeRate Decimal Exchange rate (Eg: 1.0000)
TranDateTime DateTime Actual Transaction UTC DateTime (yyyy-MM-dd HH:mm:ss) on Provider system.

**This is the actual date and time when the result were placed, verified within the
provider's game system.
ProviderTimeZone String Provider side Time Zone
ProviderTranDt DateTime Actual Transaction DateTime based on ProviderTimeZone
RoundType Integer Round Type:
(Please refer RoundType)

Example of JSON request
## JSON
## {
"OperatorId": "DemoAccount",
"RequestDateTime": "2014-09-30T14:16:32Z",
"Signature": "8d3d050acf123op78a42328215872745",
"PlayerId": "Player001"
"Currency": "MYR",
"ResultId": 438666,
"BetId": 438665,
"RoundId": 438664,
"GameCode": "10000",
"GameType": “Slots”,
"GameName": "Game 001",
"ResultType": 0,
"BetAmount": 0.2000,
"ValidBetAmount": 0.2000,
"Payout": 0.0000,
"WinLose": -0.2000,
"ExchangeRate": 1.0000,
"TranDateTime": "2014-09-30 14:16:32",
"ProviderTimeZone": "Singapore Standard Time",
"ProviderTranDt": "2014-09-30T22:16:32.000+08:00",
"RoundType": 0
## }

Response parameters
## Name Type Description
Status Integer Status code
(Please refer operator Error / Status Code Table)

Description String(50) Status description
ResponseDateTime String(50) UTC datetime (yyyy-MM-dd HH:mm:ss)

**Using current UTC+0 datetime, this field is exclusively intended for MD5 hashing
and validation purposes. Please refrain from utilising it for transactional records.
OldBalance Decimal Player’s balance before add payout (eg: 1233.5000)
NewBalance Decimal Player’s balance after added payout (eg: 1233.5000)

Example of JSON response
## JSON
## {
"Status": 200,
"Description": "Success",
"ResponseDateTime": "2016-09-01 09:41:37",
"OldBalance": 100.0000,
"NewBalance": 102.0000
## }
3.2.8 POST CancelBetNSettle
Request path: POST /CancelBetNSettle

This Api is to ensure the result is delivered to the operator. If the game round has existed, responds
success response status. If there is any error, return rejected response status, this api will attempt refire
until receive a success response status from operator’s system.

Important: Once BetNSettle is created. It cannot be void, cancel and rollback. As the result has already generated, thus this
api will refire until operator has return the winning to player.

Request parameters
## Name Type Description
OperatorId String(20) Operator Id
RequestDateTime String(50) UTC datetime (yyyy-MM-ddTHH:mm:ssZ)

**Using current UTC+0 datetime, this field is exclusively intended for MD5 hashing
and validation purposes. Please refrain from utilising it for transactional records.
Signature String(50) MD5 (FunctionName + ResultId + RequestDateTime + OperatorId + SecretKey +
PlayerId)
(Please refer MD5 hashing function)
PlayerId String(50) Player Id in operator system
Currency String(5) Eg: MYR: Malaysia Ringgit, SGD: Singapore Dollar
(Please refer Currency Code Table)

ResultId Long Unique result transaction id of the game round on provider system

**Use this value to ensure transaction uniqueness
**Apply this TranId in the 2.1.3 GetTransactionDetails method to access a
comprehensive view of the game's transaction details.
BetId Long Unique bet transaction id of the game round on provider system
RoundId Long Unique round id of the game round, multiple players may share the same round id
GameCode String(50) Unique Code of the game.
GameType String(50) Game Type in string. (Eg: Slots / Arcade)
(Please refer Game Type)
GameName String(50) English game name / description
ResultType Integer Game Result Type:
(Please refer Game Result Type)
BetAmount Decimal Bet amount (Eg: 12345678.1234)
ValidBetAmount Decimal Valid Bet amount (Eg: 12345678.1234)
Payout Decimal Payout (Eg: 12345678.1234)

**Can be 0 (‘ZERO’) value if the round doesn’t generate payout
**Use this value to update player balance
WinLose Decimal Winlose amount (Payout - Turnover)

**Can be negative value (-ve)
ExchangeRate Decimal Exchange rate (Eg: 1.0000)
TranDateTime DateTime Actual Transaction UTC DateTime (yyyy-MM-dd HH:mm:ss) on Provider system.

**This is the actual date and time when the result were placed, verified within the
provider's game system.
ProviderTimeZone String Provider side Time Zone
ProviderTranDt DateTime Actual Transaction DateTime based on ProviderTimeZone
RoundType Integer Round Type:
(Please refer RoundType)

Example of JSON request
## JSON
## {
"OperatorId": "DemoAccount",
"RequestDateTime": "2014-09-30T14:16:32Z",
"Signature": "8d3d050acf123op78a42328215872745",
"PlayerId": "Player001"
"Currency": "MYR",
"ResultId": 438666,
"BetId": 438665,
"RoundId": 438664,

"GameCode": "10000",
"GameType": “Slots”,
"GameName": "Game 001",
"ResultType": 0,
"BetAmount": 0.2000,
"ValidBetAmount": 0.2000,
"Payout": 0.0000,
"WinLose": -0.2000,
"ExchangeRate": 1.0000,
"TranDateTime": "2014-09-30 14:16:32",
"ProviderTimeZone": "Singapore Standard Time",
"ProviderTranDt": "2014-09-30T22:16:32.000+08:00",
"RoundType": 0
## }

Response parameters
## Name Type Description
Status Integer Status code
(Please refer operator Error / Status Code Table)
Description String(50) Status description
ResponseDateTime String(50) UTC datetime (yyyy-MM-dd HH:mm:ss)

**Using current UTC+0 datetime, this field is exclusively intended for MD5 hashing
and validation purposes. Please refrain from utilising it for transactional records.
OldBalance Decimal Player’s balance before add payout (eg: 1233.5000)
NewBalance Decimal Player’s balance after added payout (eg: 1233.5000)

Example of JSON response
## JSON
## {
"Status": 200,
"Description": "Success",
"ResponseDateTime": "2016-09-01 09:41:37",
"OldBalance": 100.0000,
"NewBalance": 102.0000
## }


3.3 Flow of placing bets for seamless
In the provider's seamless integration system, a bet undergoes a series of steps before generating results
for players. The process begins with the player placing a bet, followed by the provider system initiating the
3.2.1 GetBalance method to verify if the player has sufficient funds. If the player's balance is adequate,
the provider system then triggers the 3.2.2 Bet method. Upon successful deduction of the balance, the
provider system generates the result for the bet round and proceeds to settle with the operator system
using the 3.2.3 GameResult method.

Finally, the player views the outcome of the bet round on their screen.

Throughout the seamless integration process, the operator system carries the responsibility of ensuring
that balances are accurately updated using the fields specified in the respective APIs. Additionally, the
operator system must guarantee that idempotent calls are not processed more than once, to prevent
unintended duplications. Transaction uniqueness can be confirmed using the transaction id defined within
the transactional APIs.
**Please also ensure operator callback response time of less than 3 sec to ensure optimal game performance.





- Fund Transfer Wallet Integration API
The operator is empowered to leverage this API for facilitating fund transfers to players' balances within
the Game Provider's wallet ecosystem.

All requests and responses are in JSON format

All request should contain header “Content-Type: application/json”
HTTP Methods : POST

Operator ID, secret key will be provided by provider for both production and test environments

The HTTPs service URL will be furnished by the provider for both production and test
environments. It takes the form of:

https://<API service domain>/api/opgateway/v1/op/<method>
or
https://<API service domain>/api/opgateway/v1/op/<path>/<method>
https://<API service domain>/api/opgateway/v1/op/<path>/<path>/<method>

The Integration HTTP Service is securely protected.

- Requests to the service should not be initiated from player browsers (end-users).
- IP addresses must be supplied to the provider for the purpose of whitelisting.
## 4.1 Game Opening Method
The operator can obtain a valid game launch URL through the Integration API 2.2 GameLogin method.
This launch URL is applicable for opening the game in any supported web browser or webview.

4.2 API Documentation
4.2.1 POST CreatePlayer
Request path: POST /CreatePlayer
**This API will be deprecated soon
**2.2 GameLogin or 4.3 CheckBalance methods will inherently generate a player profile within the provider's system if one
does not already exist.

The CreatePlayer method for operators to establish new player accounts within the provider's system.

Request parameters
## Name Type Description Status
OperatorId String(20) Operator Id  Required
RequestDateTime String(50) UTC datetime (yyyy-MM-ddTHH:mm:ssZ)

**Using current UTC+0 datetime, this field is exclusively intended for
MD5 hashing and validation purposes. Please refrain from utilising it
for transactional records.
## Required
Signature String(50) MD5 (FunctionName + RequestDateTime + OperatorId + SecretKey +
PlayerId)
(Please refer MD5 hashing function)
## Required
PlayerId String(50) Player Id in operator system Required

Example of JSON request
## JSON
## {
"OperatorId": "DemoAccount",
"RequestDateTime": "2014-09-30T14:16:32Z",
"Signature": "8d3d050acf123op78a42328215872745",
"PlayerId": "Player001"
## }

Response parameters
## Name Type Description
Status Integer Status code
(Please refer provider Error / Status Code Table)
Description String(50) Status description
ResponseDateTime String(50) UTC datetime (yyyy-MM-dd HH:mm:ss)

**Using current UTC+0 datetime, this field is exclusively intended for MD5 hashing
and validation purposes. Please refrain from utilising it for transactional records.

Example of JSON response

## JSON
## {
"Status": 200,
"Description": "Success",
"ResponseDateTime": "2016-09-01 09:41:37"
## }
4.2.2 POST CheckBalance
Request path: POST /CheckBalance

Operators can utilise the CheckBalance method to ascertain a player's balance within the provider's
system.

Request parameters
## Name Type Description Status
OperatorId String(20) Operator Id  Required
RequestDateTime String(50) UTC datetime (yyyy-MM-ddTHH:mm:ssZ)

**Using current UTC+0 datetime, this field is exclusively intended for
MD5 hashing and validation purposes. Please refrain from utilising it
for transactional records.
## Required
Signature String(50) MD5 (FunctionName + RequestDateTime + OperatorId + SecretKey +
PlayerId)
(Please refer MD5 hashing function)
## Required
PlayerId String(50) Player Id in operator system Required

Example of JSON request
## JSON
## {
"OperatorId": "DemoAccount",
"RequestDateTime": "2014-09-30T14:16:32Z",
"Signature": "8d3d050acf123op78a42328215872745",
"PlayerId": "Player001"
## }

Response parameters
## Name Type Description
Status Integer Status code
(Please refer provider Error / Status Code Table)
Description String(50) Status description
ResponseDateTime String(50) UTC datetime (yyyy-MM-dd HH:mm:ss)


**Using current UTC+0 datetime, this field is exclusively intended for MD5 hashing
and validation purposes. Please refrain from utilising it for transactional records.
CurrentBalance Decimal Current balance in the account (Eg: 12345678.1234)
Currency String(3) Eg: MYR: Malaysia Ringgit, SGD: Singapore Dollar
(Please refer Currency Code Table)

Example of JSON response
## JSON
## {
"Status": 200,
"Description": "Success",
"ResponseDateTime": "2016-09-01 09:41:37",
"CurrentBalance": 0.00,
"Currency": "MYR"
## }
4.2.3 POST Deposit
Request path: POST /Deposit

The Deposit method, provided by the provider, enables operators to add funds to a player's account
within the provider's system.

Request parameters
## Name Type Description Status
OperatorId String(20) Operator Id  Required
RequestDateTime String(50) UTC datetime (yyyy-MM-ddTHH:mm:ssZ)

**Using current UTC+0 datetime, this field is exclusively intended for
MD5 hashing and validation purposes. Please refrain from utilising it
for transactional records.
## Required
Signature String(50) MD5 (FunctionName + RequestDateTime + OperatorId + SecretKey +
PlayerId)
(Please refer MD5 hashing function)
## Required
PlayerId String(50) Player Id in operator system Required
Amount String(50) Amount to deposit into player’s FundTransfer account (Eg: 12345678.12)

** Amounts are in the operator’s currency. For truncated currencies, the
amount needs to be converted using the truncation rate. For example: if 1
MY1 = 0.01 MYR, and a player has a balance of 100 MYR, then the
equivalent in MY1 is 100 / 0.01 = 10,000. The operator must pass 10,000
as the amount in the request.

**The provider's system accommodates up to two decimal units.
**Only positive numbers are permitted. The provider's system will
reject any incoming API calls with negative amounts.
## Required
ReferenceId String(50) Unique transaction id from operator side Required


**The ReferenceId must be unique within the operator's system. Any
duplicate reference id sent from the operator's system will be
rejected by the provider's system.

Example of JSON request
## JSON
## {
"OperatorId": "DemoAccount",
"RequestDateTime": "2014-09-30T14:16:32Z",
"Signature": "8d3d050acf123op78a42328215872745",
"PlayerId": "Player001",
"Amount": "100.00",
"ReferenceId": "13311511"
## }

Response parameters
## Name Type Description
Status Integer Status code
(Please refer provider Error / Status Code Table)
Description String(50) Status description
ResponseDateTime String(50) UTC datetime (yyyy-MM-dd HH:mm:ss)

**Using current UTC+0 datetime, this field is exclusively intended for MD5 hashing
and validation purposes. Please refrain from utilising it for transactional records.
CurrentBalance Decimal Current balance in the account (Eg: 12345678.12)

**The provider's system accommodates up to two decimal units.
Currency String(3) Eg: MYR: Malaysia Ringgit, SGD: Singapore Dollar
(Please refer Currency Code Table)

Example of JSON response
## JSON
## {
"Status": 200,
"Description": "Success",
"ResponseDateTime": "2016-09-01 09:41:37",
"CurrentBalance": 0.00,
"Currency": "MYR"
## }
4.2.4 POST Withdraw
Request path: POST /Withdraw


Operators can leverage the Withdraw method to initiate fund withdrawals from a player's account within
the provider's system.

Request parameters
## Name Type Description Status
OperatorId String(20) Operator Id  Required
RequestDateTime String(50) UTC datetime (yyyy-MM-ddTHH:mm:ssZ)

**Using current UTC+0 datetime, this field is exclusively intended for
MD5 hashing and validation purposes. Please refrain from utilising it
for transactional records.
## Required
Signature String(50) MD5 (FunctionName + RequestDateTime + OperatorId + SecretKey +
PlayerId)
(Please refer MD5 hashing function)
## Required
PlayerId String(50) Player Id in operator system Required
Amount String(50) Amount to withdraw from player’s FundTransfer account (Eg:
## 12345678.12)

** Amounts are in the operator’s currency. For truncated currencies, the
amount needs to be converted using the truncation rate. For example: if 1
MY1 = 0.01 MYR, and a player has a balance of 100 MYR, then the
equivalent in MY1 is 100 / 0.01 = 10,000. The operator must pass 10,000
as the amount in the request.

**The provider's system accommodates up to two decimal units.
**Only positive numbers are permitted. The provider's system will
reject any incoming API calls with negative amounts.
## Required
ReferenceId String(50) Unique transaction id from operator side

**The ReferenceId must be unique within the operator's system. Any
duplicate reference id sent from the operator's system will be
rejected by the provider's system.
## Required

Example of JSON request
## JSON
## {
"OperatorId": "DemoAccount",
"RequestDateTime": "2014-09-30T14:16:32Z",
"Signature": "8d3d050acf123op78a42328215872745",
"PlayerId": "Player001",
"Amount": "100.00",
"ReferenceId": "13311511"
## }

Response parameters
## Name Type Description
Status Integer Status code

(Please refer provider Error / Status Code Table)
Description String(50) Status description
ResponseDateTime String(50) UTC datetime (yyyy-MM-dd HH:mm:ss)

**Using current UTC+0 datetime, this field is exclusively intended for MD5 hashing
and validation purposes. Please refrain from utilising it for transactional records.
CurrentBalance Decimal Current balance in the account (Eg: 12345678.12)

**The provider's system accommodates up to two decimal units.
Currency String(3) Eg: MYR: Malaysia Ringgit, SGD: Singapore Dollar
(Please refer Currency Code Table)

Example of JSON response
## JSON
## {
"Status": 200,
"Description": "Success",
"ResponseDateTime": "2016-09-01 09:41:37",
"CurrentBalance": 0.00,
"Currency": "MYR"
## }
4.2.5 POST PullLog
Request path: POST /PullLog

Using this method, the operator gains the capability to retrieve players betting logs for fund transfer
wallets.
**For detailed implementation guidance, please consult section 4.3 Transaction Log Pulling Mechanism of the
documentation.

Request parameters
## Name Type Description Status
OperatorId String(20) Operator Id  Required
RequestDateTime String(50) UTC datetime (yyyy-MM-ddTHH:mm:ssZ)

**Using current UTC+0 datetime, this field is exclusively intended for
MD5 hashing and validation purposes. Please refrain from utilising it
for transactional records.
## Required
Signature String(50) MD5 (FunctionName + RequestDateTime + OperatorId + SecretKey)
(Please refer MD5 hashing function)
## Required

Example of JSON request
## JSON

## {
"OperatorId": "DemoAccount",
"RequestDateTime": "2014-09-30T14:16:32Z",
"Signature": "8d3d050acf123op78a42328215872745"
## }

Response parameters
## Name Type Description
Status Integer Status code
(Please refer provider Error / Status Code Table)
Description String(50) Status description
ResponseDateTime String(50) UTC datetime (yyyy-MM-dd HH:mm:ss)

**Using current UTC+0 datetime, this field is exclusively intended for MD5 hashing
and validation purposes. Please refrain from utilising it for transactional records.
Logs Array Transaction object array (Object field please refer following table)

**Each API call will yield a maximum of 1000 transactions.

continue.. Response parameters (Object Logs)
## Name Type Description
TranId Long Unique Id for this transaction on provider system

**Apply this TranId in the 2.1.3 GetTransactionDetails method to access a
comprehensive view of the game's transaction details.
PlayerId String(50) Player Id in operator system
Turnover Decimal Turnover amount (Eg: 12345678.1234)
ValidTurnover Decimal Valid turnover amount (Eg: 12345678.1234)
Payout Decimal Payout amount (Eg: 12345678.1234)

**Can be 0 (‘ZERO’) value if the round doesn’t generate payout
WinLose Decimal Winlose amount (Payout - Turnover)

**Can be negative value (-ve)
TranDt DateTime Actual Transaction UTC DateTime (yyyy-MM-ddTHH:mm:ssZ) on Provider side.


**This is the actual date and time when the bets were placed, verified within the
provider's game system.
TranType Integer Transaction type
(Please refer Transaction Type)
GameCode String(50) Unique code of the game within the provider system
GameType Integer Game type
(Please refer Game Type)

GameName String(50) English game name / description
ProviderTimeZone String Provider side Time Zone
ProviderTranDt DateTime Transaction Finance/Billing DateTime based on ProviderTimeZone
RoundType Integer Round type
(Please refer Round Type)

Example of JSON response
## JSON
## {
"Status": 200,
"Description": "Success",
"ResponseDateTime": "2016-09-01 09:41:37",
"Logs": [
## {
"TranId": 133133134,
"PlayerId": "DemoPlayer",
"Turnover": 3.60,
"ValidTurnover": 3.60,
"Payout": 1.80,
"WinLose": -1.80,
"TranDt": "2020-10-10T09:30:00Z",
"TranType": 0,
"GameCode": "1000",
"GameType": 1,
"GameName": "Slots Game Name",
“ProviderTimeZone”: “Singapore Standard Time”,
“ProviderTranDt”: "2024-01-02T14:55:26.1212204+08:00",
“RoundType”: 0
## },
## ...
## ]
## }
4.2.6 POST FlagLog
Request path: POST /FlagLog

Using this method, the operator gains the capability to flag retrieved records, This action serves to
prevent return of identical sets of betting logs when invoking the PullLog method.
**For detailed implementation guidance, please consult section 4.3 Transaction Log Pulling Mechanism of the
documentation.


Request parameters
## Name Type Description Status

OperatorId String(20) Operator Id  Required
RequestDateTime String(50) UTC datetime (yyyy-MM-ddTHH:mm:ssZ)

**Using current UTC+0 datetime, this field is exclusively intended for
MD5 hashing and validation purposes. Please refrain from utilising it
for transactional records.
## Required
Signature String(50) MD5 (FunctionName + RequestDateTime + OperatorId + SecretKey)
(Please refer MD5 hashing function)
## Required
TransactionIds Long[] List of pulled transaction IDs

**Limited to a maximum of 1000 transaction IDs.
## Required

Example of JSON request
## JSON
## {
"OperatorId": "DemoAccount",
"RequestDateTime": "2014-09-30T14:16:32Z",
"Signature": "8d3d050acf123op78a42328215872745",
"TransactionIds":  [133123, 133124, ...]
## }

Response parameters
## Name Type Description
Status Integer Status code
(Please refer provider Error / Status Code Table)
Description String(50) Status description
ResponseDateTime String(50) UTC datetime (yyyy-MM-dd HH:mm:ss)

**Using current UTC+0 datetime, this field is exclusively intended for MD5 hashing
and validation purposes. Please refrain from utilising it for transactional records.

Example of JSON response
## JSON
## {
"Status": 200,
"Description": "Success",
"ResponseDateTime": "2016-09-01 09:41:37"
## }
4.2.7 POST PullLogByTimestamp
Request path: POST /PullLogByTimestamp


Using this method, the operator gains the capability to retrieve players betting logs for fund transfer
wallets according to utc+0 timestamp.
**For detailed implementation guidance, please consult section 4.4 Log Pulling by Timestamp Mechanism of the
documentation.


Request parameters
## Name Type Description Status
OperatorId String(20) Operator Id  Required
RequestDateTime String(50) UTC datetime (yyyy-MM-ddTHH:mm:ssZ)

**Using current UTC+0 datetime, this field is exclusively intended for
MD5 hashing and validation purposes. Please refrain from utilising it
for transactional records.
## Required
Signature String(50) MD5 (FunctionName + RequestDateTime + OperatorId + SecretKey)
(Please refer MD5 hashing function)
## Required
FromTs Integer UTC timestamp

**Maximum 300 seconds (5 minutes) of betting logs will be return
from API
## Required
Page Integer Determine which page to pull

**Start with 1
## Required

Example of JSON request
## JSON
## {
"OperatorId": "DemoAccount",
"RequestDateTime": "2014-09-30T14:16:32Z",
"Signature": "8d3d050acf123op78a42328215872745",
"FromTs": 1691500000,
"Page": 1
## }

Response parameters
## Name Type Description
Status Integer Status code
(Please refer provider Error / Status Code Table)
Description String(50) Status description
ResponseDateTime String(50) UTC datetime (yyyy-MM-dd HH:mm:ss)

**Using current UTC+0 datetime, this field is exclusively intended for MD5 hashing
and validation purposes. Please refrain from utilising it for transactional records.
FromTs Integer Indicate current transaction logs is from and to which timestamp range
ToTs Integer Indicate current transaction logs is from and to which timestamp range


Logs Array Transaction object array (Object field please refer following table)

**Each API call will yield a maximum of 1000 transactions.

continue.. Response parameters (Object Logs)
## Name Type Description
TranId Long Unique Id for this transaction on provider system

**Apply this TranId in the 2.1.3 GetTransactionDetails method to access a
comprehensive view of the game's transaction details.
PlayerId String(50) Player Id in operator system
Turnover Decimal Turnover amount (Eg: 12345678.1234)
ValidTurnover Decimal Valid turnover amount (Eg: 12345678.1234)
Payout Decimal Payout amount (Eg: 12345678.1234)

**Can be 0 (‘ZERO’) value if the round doesn’t generate payout
WinLose Decimal Winlose amount (Payout - Turnover)

**Can be negative value (-ve)
TranDt DateTime Actual Transaction UTC DateTime (yyyy-MM-ddTHH:mm:ssZ) on Provider side.

**This is the actual date and time when the bets were placed, verified within the
provider's game system.
TranType Integer Transaction type
(Please refer Transaction Type)
GameCode String(50) Unique code of the game within the provider system
GameType Integer Game type
(Please refer Game Type)
GameName String(50) English game name / description
ProviderTimeZone String Provider side Time Zone
ProviderTranDt DateTime Transaction Finance/Billing DateTime based on ProviderTimeZone
RoundType Integer Round type
(Please refer Round Type)

Example of JSON response
## JSON
## {
"Status": 200,
"Description": "Success",
"ResponseDateTime": "2016-09-01 09:41:37",
"FromTs": 1691500000,
"ToTs": 1791500000,

"Logs": [
## {
"TranId": 133133134,
"PlayerId": "DemoPlayer",
"Turnover": 3.60,
"ValidTurnover": 3.60,
"Payout": 1.80,
"WinLose": -1.80,
"TranDt": "2020-10-10T09:30:00Z",
"TranType": 0,
"GameCode": "1000",
"GameType": 1,
"GameName": "Slots Game Name",
“ProviderTimeZone”: “Singapore Standard Time”,
“ProviderTranDt”: "2024-01-02T14:55:26.1212204+08:00",
“RoundType”: 0
## },
## ...
## ]
## }

4.2.8 POST PullLogBonus
Request path: POST /PullLogBonus

Using this method, the operator gains the capability to retrieve players Bonus logs for fund transfer
wallets.
**For detailed implementation guidance, please consult section 4.3 Transaction Log Pulling Mechanism of the
documentation.

Request parameters
## Name  Type  Description  Status
OperatorId  String(20)  Operator Id   Required
RequestDateTime  String(50)  UTC datetime (yyyy-MM-ddTHH:mm:ssZ)

**Using current UTC+0 datetime, this field is exclusively intended for MD5
hashing and validation purposes. Please refrain from utilising it for
transactional records.
## Required
Signature  String(50)  MD5 (FunctionName + RequestDateTime + OperatorId + SecretKey)
(Please refer MD5 hashing function)
## Required

Example of JSON request
## JSON
## {
"OperatorId": "DemoAccount",
"RequestDateTime": "2014-09-30T14:16:32Z",
"Signature": "8d3d050acf123op78a42328215872745"
## }

Response parameters
## Name  Type  Description
Status  Integer  Status code
(Please refer provider Error / Status Code Table)
Description  String(50)  Status description
ResponseDateTime  String(50)  UTC datetime (yyyy-MM-dd HH:mm:ss)

**Using current UTC+0 datetime, this field is exclusively intended for MD5 hashing
and validation purposes. Please refrain from utilising it for transactional records.
Logs  Array  Transaction object array (Object field please refer following table)

**Each API call will yield a maximum of 1000 transactions.

continue.. Response parameters (Object Logs)
## Name  Type  Description

TranId  Long  Unique Id for this transaction on provider system

**Apply this TranId in the 2.1.3 GetTransactionDetails method to access a
comprehensive view of the game's transaction details.
PlayerId  String(50)  Player Id in operator system
Payout  Decimal  Payout amount (Eg: 12345678.1234)

**Can be 0 (‘ZERO’) value if the round doesn’t generate payout
TranDt  DateTime  Actual Transaction UTC DateTime (yyyy-MM-ddTHH:mm:ssZ) on Provider side.

**This is the actual date and time when the bets were placed, verified within the
provider's game system.
TranType  Integer  Transaction type
(Please refer Transaction Type)
ProviderTimeZone  String  Provider side Time Zone
ProviderTranDt  DateTime  Transaction Finance/Billing DateTime based on ProviderTimeZone
RoundType  Integer  Round type
(Please refer Round Type)
AmountCoin  Long  Bonus winning coin
CurrencyCode  String  Eg: MYR: Malaysia Ringgit, SGD: Singapore Dollar
(Please refer Currency Code Table)
BonusCode  String  Unique bonus codes represent different bonus types.
BonusName  String  Cash bonus Reward Name
BonusResult  String  Cash bonus Result
(Please refer Result)

Example of JSON response
## JSON

## {
"Status": 200,
"Description": "Success",
"ResponseDateTime": "2016-09-01 09:41:37",
"Logs": [
## {
"TranId": 133133134,
"PlayerId": "DemoPlayer",
"Payout": 1.80,
"TranDt": "2020-10-10T09:30:00Z",
"TranType": 0,
“ProviderTimeZone”: “Singapore Standard Time”,
“ProviderTranDt”: "2024-01-02T14:55:26.1212204+08:00",
“RoundType”: 0,
“AmountCoins”: 5000,
“CurrencyCode”: “MYR”,
“BonusCode”: “UUSA”,
“BonusName”: “Angpau”,
“BonusResult”: “Angpau”
## },
## ...
## ]
## }
4.2.9 POST FlagLogBonus
Request path: POST /FlagLogBonus

Using this method, the operator gains the capability to flag retrieved bonus records, This action serves to
prevent return of identical sets of betting bonus logs when invoking the PullLogBonus method.
**For detailed implementation guidance, please consult section 4.3 Transaction Log Pulling Mechanism of the
documentation.

Request parameters
## Name  Type  Description  Status
OperatorId  String(20)  Operator Id   Required
RequestDateTime  String(50)  UTC datetime (yyyy-MM-ddTHH:mm:ssZ)

**Using current UTC+0 datetime, this field is exclusively intended for MD5
hashing and validation purposes. Please refrain from utilising it for
transactional records.
## Required
Signature  String(50)  MD5 (FunctionName + RequestDateTime + OperatorId + SecretKey)
(Please refer MD5 hashing function)
## Required
TransactionIds  Long[]  List of pulled transaction IDs

**Limited to a maximum of 1000 transaction IDs.
## Required

Example of JSON request
## JSON

## {
"OperatorId": "DemoAccount",
"RequestDateTime": "2014-09-30T14:16:32Z",
"Signature": "8d3d050acf123op78a42328215872745",
"TransactionIds":  [133123, 133124, ...]
## }

Response parameters
## Name  Type  Description
Status  Integer  Status code
(Please refer provider Error / Status Code Table)
Description  String(50)  Status description
ResponseDateTime  String(50)  UTC datetime (yyyy-MM-dd HH:mm:ss)

**Using current UTC+0 datetime, this field is exclusively intended for MD5 hashing
and validation purposes. Please refrain from utilising it for transactional records.

Example of JSON response
## JSON
## {
"Status": 200,
"Description": "Success",
"ResponseDateTime": "2016-09-01 09:41:37"
## }
4.2.10 POST PullLogBonusByTimestamp
Request path: POST /PullLogBonusByTimestamp

Using this method, the operator gains the capability to retrieve players betting bonus logs for fund transfer
wallets according to utc+0 timestamp.
**For detailed implementation guidance, please consult section 4.4 Log Pulling by Timestamp Mechanism of the
documentation.

Request parameters
## Name  Type  Description  Status
OperatorId  String(20)  Operator Id   Required
RequestDateTime  String(50)  UTC datetime (yyyy-MM-ddTHH:mm:ssZ)

**Using current UTC+0 datetime, this field is exclusively intended for MD5
hashing and validation purposes. Please refrain from utilising it for
transactional records.
## Required
Signature  String(50)  MD5 (FunctionName + RequestDateTime + OperatorId + SecretKey)
(Please refer MD5 hashing function)
## Required

FromTs  Integer  UTC timestamp

**Maximum 300 seconds (5 minutes) of betting logs will be return from API
## Required
Page  Integer  Determine which page to pull

**Start with 1
## Required

Example of JSON request
## JSON
## {
"OperatorId": "DemoAccount",
"RequestDateTime": "2014-09-30T14:16:32Z",
"Signature": "8d3d050acf123op78a42328215872745",
"FromTs": 1691500000,
"Page": 1
## }

Response parameters
## Name  Type  Description
Status  Integer  Status code
(Please refer provider Error / Status Code Table)
Description  String(50)  Status description
ResponseDateTime  String(50)  UTC datetime (yyyy-MM-dd HH:mm:ss)

**Using current UTC+0 datetime, this field is exclusively intended for MD5 hashing
and validation purposes. Please refrain from utilising it for transactional records.
FromTs  Integer  Indicate current transaction logs is from and to which timestamp range
ToTs  Integer  Indicate current transaction logs is from and to which timestamp range


Logs  Array  Transaction object array (Object field please refer following table)

**Each API call will yield a maximum of 1000 transactions.

continue.. Response parameters (Object Logs)
## Name  Type  Description
TranId  Long  Unique Id for this transaction on provider system

**Apply this TranId in the 2.1.3 GetTransactionDetails method to access a
comprehensive view of the game's transaction details.
PlayerId  String(50)  Player Id in operator system

Payout  Decimal  Payout amount (Eg: 12345678.1234)

**Can be 0 (‘ZERO’) value if the round doesn’t generate payout
TranDt  DateTime  Actual Transaction UTC DateTime (yyyy-MM-ddTHH:mm:ssZ) on Provider side.

**This is the actual date and time when the bets were placed, verified within the
provider's game system.
TranType  Integer  Transaction type
(Please refer Transaction Type)
ProviderTimeZone  String  Provider side Time Zone
ProviderTranDt  DateTime  Transaction Finance/Billing DateTime based on ProviderTimeZone
RoundType  Integer  Round type
(Please refer Round Type)
AmountCoin  Long  Bonus winning coin
CurrencyCode  String  Eg: MYR: Malaysia Ringgit, SGD: Singapore Dollar
(Please refer Currency Code Table)
BonusCode  String  Unique bonus codes represent different bonus types.
BonusName  String  Cash bonus Reward Name
BonusResult  String  Cash bonus Result
(Please refer Result)

Example of JSON response
## JSON
## {
"Status": 200,
"Description": "Success",
"RequestDateTime": "2014-09-30T14:16:32Z",
"FromTs": 1691500000,
"ToTs": 1791500000,
"Logs": [
## {
"TranId": 133133134,
"PlayerId": "DemoPlayer",
"Payout": 1.80,
"TranDt": "2020-10-10T09:30:00Z",
"TranType": 0,
“ProviderTimeZone”: “Singapore Standard Time”,
“ProviderTranDt”: "2024-01-02T14:55:26.1212204+08:00",
“RoundType”: 0,
“AmountCoins”: 5000,
“CurrencyCode”: “MYR”,
“BonusCode”: “UUSA”,
“BonusName”: “Angpau”,

“BonusResult”: “Angpau”
## },
## ...
## ]
## }

4.2.11 POST CheckTransferStatus
Request path: POST /CheckTransferStatus

Operators can utilise the CheckTransferStatus method to ascertain a player's deposit and withdrawal
statement within the provider's system.

Request parameters
## Name Type Description Status
OperatorId String(20) Operator Id  Required
RequestDateTime String(50) UTC datetime (yyyy-MM-ddTHH:mm:ssZ)

**Using current UTC+0 datetime, this field is exclusively intended for
MD5 hashing and validation purposes. Please refrain from utilising it
for transactional records.
## Required
Signature String(50) MD5 (FunctionName + RequestDateTime + OperatorId + SecretKey +
PlayerId + ReferenceId + TransferType)
(Please refer MD5 hashing function)
## Required
PlayerId String(50) Player Id in operator system Required
ReferenceId String(50) Unique transaction id from operator side

**The ReferenceId must be unique within the operator's system. Any
duplicate reference id sent from the operator's system will be
rejected by the provider's system.
## Required
TransferType Integer Transfer type (1:Deposit, 2:Withdrawal) Required

Example of JSON request
## JSON
## {
"OperatorId": "DemoAccount",
"RequestDateTime": "2014-09-30T14:16:32Z",
"Signature": "8d3d050acf123op78a42328215872745",
"PlayerId": "Player001",
"ReferenceId": "13311511",
"TransferType": 1
## }

Response parameters
## Name Type Description

Status Integer Status code
(Please refer provider Error / Status Code Table)
Description String(50) Status description
ResponseDateTime String(50) UTC datetime (yyyy-MM-dd HH:mm:ss)

**Using current UTC+0 datetime, this field is exclusively intended for MD5 hashing
and validation purposes. Please refrain from utilising it for transactional records.
Trans obj Deposit / Withdrawal Transaction object
continue.. Response parameters (Object Logs)
## Name  Type  Description
TranId  Long  Unique Id for this transaction on provider system
Amount Decimal  Deposit / Withdrawal Amount (Eg: 2000)
PrevBalance Decimal  Previous Amount (Eg: 12345678.1234)
NewBalance Decimal  New Amount (Eg: 12345678.1234)


Example of JSON response
## JSON
## {
"Status": 200,
"Description": "Success",
"ResponseDateTime": "2016-09-01 09:41:37",
"Trans": {
"TranId": "123456",
"Amount": "1000",
"PrevBalance": "0",
"NewBalance": "1000"
## }
## }




## 4.3 Transaction Log Pulling Mechanism
The Fund Transfer wallet provides a log-pulling method through the 4.2.5 PullLog/4.2.8 PullLogBonus and
4.2.6 FlagLog/4.2.9 FlagLogBonus methods. These methods facilitate the retrieval of players' betting
logs. While optional, operators are mandated to implement them to receive player betting logs. This
process involves a series of steps that must be followed accurately to ensure the correct acquisition of the
betting logs.


## Step 1:
Operator initiates the process of fetching betting logs by invoking the PullLog API.

## Step 2:
Provider's system returns a maximum of 1000 unflagged betting logs.

## Step 3:
Operator receives the betting logs and subsequently performs internal processes, which may involve
inserting or summarising transactions.

## Step 4:
Operator initiates the FlagLog process to mark transactions within the provider's system as flagged or
processed. This action helps prevent the re-pulling of the same transactions during subsequent retrieval
attempts.

If the operator encounters difficulty in processing certain transactions, they have the option to exclude
those transactions from insertion in the FlagLog method. This choice allows the transactions to be
retrieved once more during the subsequent pull process.

## Step 5:

Upon successful execution of the FlagLog method by the provider's system, the operator's system may
proceed to repeat step 1: initiating the PullLog API. This facilitates the retrieval of the next batch of
transactions.

It is recommended that the operator considers waiting for an additional 5-10 seconds before initiating the
next PullLog if the method returns fewer than 1000 betting logs. This practice assists in alleviating the
load on the provider's system.

4.4 Log Pulling by Timestamp Mechanism
The Fund Transfer wallet provides a log-pulling by timestamp method through the 4.2.7
PullLogByTimestamp. This method facilitates the retrieval of players' betting logs from specific
timestamps. While optional, operators are mandated to implement them to receive player betting logs.
This process involves a series of steps that must be followed accurately to ensure the correct acquisition
of the betting logs.

## Step 1:
Operator initiates the process of fetching betting logs by invoking the PullLogByTimestamp API.

## Step 2:
Provider's system returns a maximum of 1000 unflagged betting logs.


## Step 3:
Operator receives the betting logs and subsequently performs internal processes, which may involve
inserting or summarising transactions.

## Step 4:
Operator should check whether the transaction array has more than 0 entries, indicating the possibility of
additional betting logs on subsequent pages. If true, the operator should initiate the API again by
incrementing the Page by 1.

It is recommended that the operator considers waiting for an additional 5-10 seconds before initiating the
next PullLogByTimestamp if the method returns 0 betting logs. This practice assists in alleviating the load
on the provider's system.

## 5. Reconciliation
If a request times out because of internet connection problems, or contains relevant error code (refer
status / error codes), then the provider system will follow a process described below, to reconcile the
action.

Important: In scenarios where the Operator encounters retry API calls within the reconciliation process, it is imperative to
ensure that transactions with the same reference id or transaction id are not processed more than once. The Operator can
implement the use of appropriate error codes to halt the reconciliation process effectively.
## 5.1 Bet Transaction
When the placement of a bet encounters a failure, the provider system will initiate a rollback. It's important
to note that no reconciliation process is applied to Bet transactions in such cases.
## 5.2 Rollback Transaction
Upon failing to receive an appropriate response from the operator system after several (3) attempts, a
rollback request will be enqueued in the background transaction queue. The reconciliation process
commences from this point.

Additionally, the operator system will periodically receive rollback requests once every hour,
autonomously and independently of ongoing game sessions. This periodicity ensures the accurate
delivery of such transactions.

The operator system retains the capability to reply with either a "rollback success" confirmation or an error
message such as "transaction not found," indicating that the provider system has effectively terminated
the transaction.
## 5.3 Game Result Transaction
Once the game result is generated within the provider's system, there's a chance that the game result or
settlement transaction could face difficulties in reaching the operator system. In case of such
occurrences, the system will make three (3) retry attempts before routing these transactions to the
reconciliation process.

It's imperative to recognize that settled transactions are irreversible and cannot be cancelled. The
provider's system is equipped with an autonomous job that engages in continuous retry attempts,
happening every hour, to ensure the successful delivery of game result transactions to the operator
system.
## 5.4 Bonus Transaction
The bonus transaction requests will undergo similar retry mechanisms as described earlier for game
result transactions.



- MD5 Hashing
## 6.1 For C#
c#
using System;
using System.Security.Cryptography;
using System.Text;

class Program
## {
static void Main()
## {
string functionName = "GameLogin";
string requestDateTime = "2023-06-09 12:34:56";
string operatorId = "op1";
string secretKey = "ABC123";
string playerId = "player123";

// Concatenate the values
string stringToHash = functionName + requestDateTime + operatorId + secretKey + playerId;

// Create an instance of the MD5 class
MD5 md5 = MD5.Create();

// Compute the hash as a byte array
byte[] hashBytes = md5.ComputeHash(Encoding.UTF8.GetBytes(stringToHash));

// Convert the byte array to a hexadecimal string
StringBuilder sb = new StringBuilder();
for (int i = 0; i < hashBytes.Length; i++)
## {
sb.Append(hashBytes[i].ToString("x2")); // "x2" formats each byte as a two-digit hexadecimal number
## }

string hash = sb.ToString();

Console.WriteLine(hash);
## }
## }

## 6.2 For Javascript
javascript
const functionName = "GameLogin";
const requestDateTime = "2023-06-09 12:34:56";
const operatorId = "op1";
const secretKey = "ABC123";
const playerId = "player123";

// Concatenate the values
const stringToHash = functionName + requestDateTime + operatorId + secretKey + playerId;

// Generate the MD5 hash
const hash = md5(stringToHash);

console.log(hash);
6.3 For PHP
php
## <?php
$functionName = "GameLogin";
$requestDateTime = "2023-06-09 12:34:56";
$operatorId = "op1";
$secretKey = "ABC123";
$playerId = "player123";

// Concatenate the values
$stringToHash = $functionName . $requestDateTime . $operatorId . $secretKey . $playerId;

// Generate the MD5 hash
$hash = md5($stringToHash);

echo $hash;
## ?>
## 6.4 For Python
python
import hashlib

functionName = "GameLogin"

requestDateTime = "2023-06-09 12:34:56"
operatorId = "op1"
secretKey = "ABC123"
playerId = "player123"

# Concatenate the values
stringToHash = functionName + requestDateTime + operatorId + secretKey + playerId

# Generate the MD5 hash
hash = hashlib.md5(stringToHash.encode()).hexdigest()

print(hash)
## 6.5 For Bash
bash
## #!/bin/bash

functionName="GameLogin"
requestDateTime="2023-06-09 12:34:56"
operatorId="op1"
secretKey="ABC123"
playerId="player123"

stringToHash="${functionName}${requestDateTime}${operatorId}${secretKey}${playerId}"

# Generate the MD5 hash
hash=$(echo -n "$stringToHash" | md5sum | cut -d' ' -f1)

echo $hash
## 6.6 For Ruby
ruby
require 'digest/md5'

function_name = "GameLogin"
request_date_time = "2023-06-09 12:34:56"
operator_id = "op1"
secret_key = "ABC123"
player_id = "player123"


# Concatenate the values
string_to_hash = function_name + request_date_time + operator_id + secret_key + player_id

# Generate the MD5 hash
hash_value = Digest::MD5.hexdigest(string_to_hash)

puts hash_value
## 6.7 For Java
java
import java.security.MessageDigest;
import java.security.NoSuchAlgorithmException;

public class HashGenerator {

public static void main(String[] args) throws NoSuchAlgorithmException {
String functionName = "GameLogin";
String requestDateTime = "2023-06-09 12:34:56";
String operatorId = "op1";
String secretKey = "ABC123";
String playerId = "player123";

// Concatenate the values
String stringToHash = functionName + requestDateTime + operatorId + secretKey + playerId;

// Generate the MD5 hash
String hashValue = generateMD5Hash(stringToHash);

System.out.println(hashValue);
## }

public static String generateMD5Hash(String input) throws NoSuchAlgorithmException {
MessageDigest md = MessageDigest.getInstance("MD5");
byte[] bytes = md.digest(input.getBytes());
StringBuilder result = new StringBuilder();

for (byte b : bytes) {
result.append(String.format("%02x", b));
## }

return result.toString();
## }
## }

## 6.8 For Swift
swift
import Foundation
import CommonCrypto

func generateMD5Hash(_ input: String) -> String {
let data = input.data(using: .utf8)!
var digest = [UInt8](repeating: 0, count: Int(CC_MD5_DIGEST_LENGTH))

_ = data.withUnsafeBytes { bytes in
CC_MD5(bytes.baseAddress, CC_LONG(data.count), &digest)
## }

return digest.map { String(format: "%02hhx", $0) }.joined()
## }

let functionName = "GameLogin"
let requestDateTime = "2023-06-09 12:34:56"
let operatorId = "op1"
let secretKey = "ABC123"
let playerId = "player123"

// Concatenate the values
let stringToHash = functionName + requestDateTime + operatorId + secretKey + playerId

// Generate the MD5 hash
let hashValue = generateMD5Hash(stringToHash)

print(hashValue)
## 6.9 For Kotlin
kotlin
import java.security.MessageDigest

fun generateMD5Hash(input: String): String {
val bytes = input.toByteArray()
val md5 = MessageDigest.getInstance("MD5")
val digest = md5.digest(bytes)
return digest.joinToString("") { "%02x".format(it) }
## }

fun main() {

val functionName = "GameLogin"
val requestDateTime = "2023-06-09 12:34:56"
val operatorId = "op1"
val secretKey = "ABC123"
val playerId = "player123"

// Concatenate the values
val stringToHash = "$functionName$requestDateTime$operatorId$secretKey$playerId"

// Generate the MD5 hash
val hashValue = generateMD5Hash(stringToHash)

println(hashValue)
## }



## 7. Appendix
## 7.1 Supported Language Code
## Language Language Code
English en-us
Chinese (simplified) zh-cn
Chinese (traditional) zh-tw
Thai th-th
Vietnamese vi-vn
Tagalog (Philippines) fil-ph
Indonesian id-id
Malay ml-my
Burmese (Myanmar) my-mm
Khmer (Cambodia) km-kh
Japanese ja-jp
Korean ko-kr
Hindu (India) hi-in
Bengali (Bangladesh) bn-bl
Nepal ne-ne
Urdu (Pakistan) ur-pk
Sri Lanka si-sl
Portuguese pt-pt
German de-de
Spanish es-es
Maltese mt-mt
Swedish sv-se
Finnish fi-fl
Norwegian nb-no
Irish ga-ie
Dutch nl-nl
Danish da-dk

## 7.2 Supported Currency Code
## Currency Code Description
MYR Malaysia Ringgit
THB Thai Baht
SGD Singapore Dollar
USD United States Dollar
VND Vietnamese Dong
VNK Vietnamese Dong (Truncated 1 VNK : 1000 VND)
IDR Indonesian Rupiah
IDK Indonesian Rupiah (Truncated 1 IDK : 1000 IDR)
MMK Myanmar Kyat
MK1 Myanmar Kyat (Truncated 1 MK1 : 100 MMK)
HKD Hong Kong Dollar
BDT Bangladeshi Taka
RMB RenMinBi
INR Indian Rupee
PKR Pakistani Rupee
AUD Australian Dollar
KRW Korean Won
KRK Korean Won (Truncated 1 KRK = 100 KRW)
LAK Laotian Kip
LKK Laotian Kip (Truncated 1 LKK = 1000 LAK)
NPR Nepalese Rupee
PHP Philippine Peso
TWD Taiwan Dollar
KHR Cambodian riel
CAD Canadian Dollar
BRL Brazilian Real
NGN Nigeria Naira
BND Brunei Dollar
EUR Euro

JPY Japan Yen
GBP Great Britain Pound
SEK Swidish Krona
NOK Norwegian Krone
DKK Danish Krone
MKK Myanmar Kyat (Truncated 1 MKk : 1000 MMK)
AED UAE Dirham
CHF Swiss Franc
LKR Sri Lankan Rupee
NZD New Zealand Rollar
RUB Russian Ruble
TRY Turkish Lira
ZAR South African Rand
MXN   Mexican Peso
MNT Mongolian Tugrik
** Any special currency request, please liaise with the Provider Team.
## 7.3 Status / Error Code
7.3.1 Status Code from Provider
## Status Code Description
## 200 OK
## 400 Bad Request
## 403 Forbidden Access
## 503 Service Maintenance
## 504 Game Maintenance
## 900300 Not Eligible
900401 Invalid Operator ID
## 900402 Invalid Player
## 900403 Invalid Signature
## 900404 Invalid Game Id
900408 Invalid TranID

## 900500 Internal Server Error
(Applied to any other errors/situations which are not in the list)
7.3.2 Status Code from Operator
## Status Code Description
## 200 OK
900404 Invalid player / password. Please try again
900405 Operator ID Error
## 900406 Incoming Request Info Incomplete
## 900407 Invalid Signature
## 900409 Duplicate Transaction
## 900415 Bet Transaction Not Found
## 900416  Player Inactive
900417 CancelBetNSettle Rejected
## 900605 Insufficient Balance
## 900500 Internal Server Error
## 800401 Max Payout Reached

**The operator can employ this error code to signify that a player has attained the maximum
winning limit on the operator's platform.

7.4 Game Type (Game Category)
Game Type Game Type in String
## 0 Others
## 1 Slots
## 2 Arcade
## 3 Table
## 4 Event
## 5 Mini Game
## 6 Fish Arcade
101  Cash Bonus (Deprecated)


## 7.5 Game Result Type
Game Type Game Type in String
## 0 Single / Quick Game Round Result
## 7.6 Rollback Type
Game Type Game Type in String
## 1 Single / Quick Game Refund

## 7.7 Round Type
Round Type Round Type in String
## 0 Normal Round
1 Buy FreeSpin/Feature Round
150 PVP Bonus Battle
## 7.8 Transaction Type
Round Type Round Type in String
## 0 Base
## 2 Bonus
## 7.9 Bonus Type
Round Type Round Type in String
## 0 None
## 2 Angpao
## 3 Event
4 FreeRound
## 8.0 Result
Round Type Round Type in String
4 gameName|minLineBet|noOfLine|betValue|gameId|freeRoundId

Others gameName|minLineBet|noOfLine|betValue
