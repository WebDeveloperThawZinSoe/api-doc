JiLi
API Manual
Revision history
Date Version Editor Change log
2025/12/12 1.0.39 Peter
Update the descriptions of the offline payments (§4.2.4):
there could be multiple offline payments for one trigger
round.
2025/12/9 1.0.38 Joe 1. GetGameList adds a sorting parameter(§3.1.6)
2025/11/1 7 1.0.37 可珺^ 1.^ Adjust example parameters Appendix F –^ Testing Tools^
2025/11/6 1.0.36 Vincent^ 1.^ Deprecate GetFreeSpinDashflow(§3.2.5)^
2025/9/25 1.0.35 Vincent^ 1.^ Add CreateSpinBonus(§3.2.11)^
2025/9/12 1.0.34 Vincent^ 1.^ Update Appendix C –^ Statement Types^
2025/8/1 3 1.0.33 可珺^ 1.^ Add smResult for /bet(§4.2.3)^ and /sessionBet^ (§4.2.7)^
2025/8/1 3 1.0.32 Vincent^ 1.^ FreeSpinData (§4.2.4)^ add skipRidReferenceId parameter^
2025/8/8 1.0.31 Vincent^ 1.^ Remove Urdu in Appendix A –^ Language Codes^
2025/8/5 1.0.30 Mark^

GetBetRecordSummary add new response
parameters(§3.1.4)
2025/5/7 1.0.29 Vincent^
Modify GetFreeSpinSendDetail (§3.2.3) to version 2
Add GetGameBetList(§ 3 .2.10)
FreeSpinData add new parameters(§4.2.4)
2025/2/24 1.0.28 Vincent^
GetFreeSpinRecordByTime(§3.2.4) add ‘Type’ parameter
GetFreeSpinRecordByReferenceID (§3.2.6) add ‘Type’
parameter
2 025/2/ 3 1 .0.27 可珺^ 1.^ Add^ /singleWallet/LoginWithoutRedirect(§2.1.1)^ ErrorCode^
2024/10/28 1.0. 26 Tyler^ 1.^ Delete /singleWallet/Login^ API^
2024/9/4 1.0. 25 Tyler^ 1.^ Deprecation notice for the login API^
2024/ 8 / 12 1.0.2 4 Tyler^
Delete 3.1.9 /api1/GetUserBetRecordByTime
Adjust disableFullScreen parameter
2024/7/4 1.0.23 Tyler^
/singleWallet/Login(§2.1.1),
/singleWallet/LoginWithoutRedirect(§2.1.2): Add parameter
to disable full screen mode
/api1/GetUserBetRecordByTime (§3.1.9): Change Account
Require to Yes
2024/6/17 1.0.22 Peter^ 1.^ Update Appendix C –^ Statement Types^
2024/5/10 1.0.21 Peter^
Add balance formula for /bet (§4.2.3) and /cancelBet (§4.2.5)
Add more details of /sessionBet (§4.2.7)
2024/5/6 1.0.20 Tyler^
Add GetUserBetRecordByTime (§3.1.9)
Update API method (use POST for all)
Index
Basic API Flow
0 Settings and precautions
API Protocols, Encryption and Decryption
- Requests and Responses
- Generate the Key
- Samples of Key Generation
Enter the game
- LoginWithoutRedirect
APIs
- Kick member
- Kick All Members (logout all members from one or all games)
- Get url link of a game detail record
- Get summary of bet records
- Query single game record (deprecated)
- Query game list
- Query MustHitBy
- Query member status
3.2. Free Spins
- Give free spins to a member
- Query overview of free spins
- Query the detail of free spins were given
- Query game records of free spins
- Query free spin usage records(deprecated)
- Query game records of FreeSpin by ReferenceID
- Cancel the given rounds of free spin
- Cancel the player’s rounds of free spin
- Give free spins to multiple members
- Query the bet amount for free spins
- Give spin bonus to a member..........................................................................................................
APIs Provided by the Operator
4.1. API Protocol and Authentication
- Authentication (optional)
- Response
4.2. APIs
- Generate the Token
- Player Authentication
- Player Bet (place bet and settlement together)
- Special Bets
Offline payments
Free Spins
Cancel Bet (rollback the bet and settlement)
Resend Bet
Sessional Bet (place bet and settle separately)
Turnover (effective bet amount)
Preserve (pre-deducted deposit amount)
Cancel Sessional Bet (rollback the bet)...........................................................................................
Appendix A – Language Codes
Appendix B – Currency Codes
Appendix C – Statement Types
Appendix D – Game Categories
Appendix E – Extra Authentications
- HTTP Basic Authentication
- Offline mode (optional)
Appendix F – Testing Tools
Query Samples
Actually calling the operator-provided API
Basic API Flow
Operator Game Provider

Login
auth
(response)
bet
(response)
bet
(response)

cancelBet

cancelBet
bet
(response)
(response)
(response)
0 Settings and precautions
Each AgentId represents an agent/client/site of the operator.
Please contact the game provider to create AgentId. English alphabets, numbers and the underscore are
allowed.
Duplicated member accounts are not allowed between different AgentIds if the same AgentKey is used.
We suggest adding prefix to the member account.
For example, if the agent WYZ_ABET has created i.e. Login (§2.1.1) a member johndoetest123 , it is
not allowed to create/Login another johndoetest123 by another agent WYZ_ZBET.
The game id will provider by our operating partner.
The DB timezone use UTC +7.
Required Information.

<api_url> operation API domain.(require)
username verfy account used for HTTP Basic Authentication (option)
password verify password used for HTTP Basic Authentication(option)
1. API Protocols, Encryption and Decryption
Requests and Responses
Following parameters are required for all requests:
Parameter Type Description
AgentId string Unique ID of the agent
Key string Validation Key (see in §1.1.2)
If HTTP POST is used as the request, please use x-www-form-urlencoded to pass the parameters.

Each response contains following parameters:
Parameter Type Description
ErrorCode string Status code of the response
Message string Status description of the response
Data Object Response data
The response from the game provider is formatted as JSON.

Generate the Key
Key = { 6 any characters } + MD5( All request parameters + KeyG) + { 6 any characters }
6 any characters: Generated randomly, no necessary to be the same between the front and the rear, and
will be ignored by the finalverification algorithm.
All request parameters：Concantrate API parameters by the format: key1=value1&key2=value2:
Note: always append AgentId=xxx to the request parameter string
Sample: Login (§2.1.1), Account, GameId, Lang, HomeUrl, Platform are listed; only Account, GameId,
Lang are used to generate the key. Concentrate them by the order in the table and append AgentId, the
result is
Account=Test1&GameId= 1 01&Lang=zh-CN&AgentId=
KeyG = MD5(DateTime.Now.ToString(“yyMMd”) + AgentId + AgentKey)
DateTime.Now = Current time ( UTC- 4 ) and formatted as “yyMMd”
◼ Year: the last two digits of Common Era
◼ Month: two digits. For example, January is 01 and February is 02.
◼ Day: one or two digits. Use 1~9 instead of 01~09.
For example, if query at 2018/9/30 10:00 UTC+7:00 a.k.a. 2018/9/29 21:00 UTC-4:00, the date string
is 180929.
Note: the day part of the date should be one-digit if it is less than 10
Sameple：2018/2/7 => 18027（use 7 instead of 07）
2018/2/18 => 180218
Samples of Key Generation
Note : The AgentId “Chaiyo_1” is just a sample. Please confirm with the Game Provider for actual AgentId.

Case 1: The generation of KeyG
Name Value
AgentKey be8e08f95357d215921f91c6a533f74d3194de
AgentId abcd_RMB^
Encryption
time 2019/01/^
string now = Datetime.Now.ToString("yyMMd"); // 2019/01/01 => "19011"
string agentId = "abcd_RMB";
string agentKey = "be8e08f95357d215921f91c6a533f74d3194de52";
string keyG = MD5(now + agentId + agentKey);

KeyG
= MD5(“19011abcd_RMBbe8e08f95357d215921f91c6a533f74d3194de52”)
= 9424ffdd6de016a5f90a97a55d99c

Case 2: Login.api
Name Value
Account Test
GameId 1
Lang zh-CN
string keyG = "9424ffdd6de016a5f90a97a55d99c717"
string querystring = "Token=Test006&GameId=1&Lang=zh-CN&AgentId=abcd_RMB";
string md5string = MD5(queryString + keyG);

string randomText1 = " 123456 "; // Random
string randomText2 = "abcdef"; // Random

string key = randomText1 + md5string + randomText2;

md5string
= MD5("Token=Test006&GameId=1&Lang=zh-CN&AgentId=abcd_RMB9424ffdd6de016a5f90a97a55d99c717”)
= 3e4c3b321eac16f20633f683be08d

Key = " 123456 3e4c3b321eac16f20633f683be08d237abcdef "

Name Result
md5string 3e4c3b321eac16f20633f683be08d
Key 1234563e4c3b321eac16f20633f683be08d237abcdef
LoginUrl
<API URL>/Login?Token=Test006&GameId=1&Lang=zh-CN&AgentId=abcd_RMB
&Key=1234563e4c3b321eac16f20633f683be08d237abcdef
2. Enter the game
LoginWithoutRedirect
URL /singleWallet/LoginWithoutRedirect Method POST Return JSON
Description Guide members into the game.(response launch game url)

Request:

Parameter Type Require Description
Token string Yes Api access token From site (800 characters at most)
GameId int Yes
Game unique identification value
(see the game list)
Lang string Yes UI language (see Appendix A)
HomeUrl string No
The URL redirect to after the player logout a game
Ignored when generating the key.
Platform string No
Platform information. See §4.2.3 and §4.2.7.
Ignored when generating the key.
disableFullScreen int No
When disableFullScreen is set to 1, full screen mode will be
disabled.
Ignored when generating the key.
The token is generated by the operator and used for the queries to the game provider. The Login API will
validate and return the account of the member. The account will be created of the member’s first time login.

Response:

Parameter Type Require Description
Data string Yes
Web link to enter the game
P.S. This link is encoded by JSON, please use JSON
decoding to extract it. This link can be used only once.
Error code:

Error Code Message Description
2 Invalid Key Key auth failed (see §1.1.2)
9
api auth fail Token verify failed when calling the operator’s
‘auth’
9 Site master not found Invalid AgentId (see Chapter 0 )
9
Site master mismatched Player account mismatches to AgentId (see
Chapter 0 )
104
invalid currency from auth The operator returns an invalid currency in the
auth
Sample of the request
/singleWallet/LoginWithoutRedirect

Token=Test001&GameId= 1 &Lang=en-US&AgentId=abcd_THB&Key=000000b7caea5de85c5e829bc88b56e15cd
fa

Sample of the response body
{
"ErrorCode": 0 ,
"Message": "success",
"Data": "https://www.xxxxx.com/fish/index.html?ssoKey=e79576885ebfc13084bf46a2e
b121f31ff37\u0026lang=en-US\u0026gameID=1"

}
3. APIs
Kick member
URL /api1/KickMember Method POST Return JSON
Description Kick the specific member,

Request:

Parameter Type Require Description
Account string Yes Unique account name
Error code:

Error Code Message Description
0 Success success
101 Invalid Member Member not existed/not online
Kick All Members (logout all members from one or all games)
URL /KickMemberAll Method POST Return JSON
Description Logout all members from the game forcibly.

Request:

Parameter Type Require Description
GameId int No Member unique identification value.
Error code:
Error Code Message Description
0 Success Logout successful

Sample QueryString：

//Logout all members
AgentId=Chaiyo_

//Logout all members in game id = 1
GameId= 1 &AgentId=Chaiyo_

Get url link of a game detail record
URL <API URL>/GetGameDetailUrl Method POST Return JSON
Description
Get url link of a game detail record.
P.S. This link is one-off and cannot be accessed again.

Request:

Parameter Type Require Description
WagersId bigint Yes Game record unique id.
Lang string No
Language used for the web page to show the detail record.
Following can be used: zh-CN, zh-TW, en-US, th-TH,
id-ID, vi-VN
If this parameter is not given or cannot be recognized,
“th-TH” will be used.
Note: please ignore Lang when generating the key.

Response:
Parameter Type Require Description
Url string Yes The url link of the game detail record.

Error code:

Error Code Message Description
0 Success Success
101 Record Not Exist Game record not exist
Sample of the request
/GetGameDetailUrl

WagersId= 987654321 &AgentId=abcd_THB&Key=00000027521e5e5f46acb9ad81c129d7f4dd2e

Sample of the response body

{
"ErrorCode": 0 ,
"Message": "success",
"Data": {
"Url":"https://www.xxxxx.com/en-US/ingame/gamehistory?token=0adf022bc84b
db4a201b8a7bbc2280aaeea41\u0026ri= 987654321 \u0026li= 987654321 "
}
}

Get summary of bet records
URL /GetBetRecordSummary Method POST Return JSON
Description Get summary of bet records by specific time range

Request:

Parameter Type Require Description
StartTime DateTime Yes Start time
EndTime DateTime Yes End time
GameId int No
Game unique id.
If not given, summary of all games will be returned.
P.S. please ignore when generating the key.
Currency string No
Currency code.
If not given, summary BY each currency will be returned.
P.S. please ignore when generating the key.
FilterAgent bool No
Filter records which not belong to the agent
If not given, summary of all agents will be returned.
P.S. please ignore when generating the key.
GroupByGame int No
Group the query results by game.
0 or not given = not group by game
1 = group by game
P.S. please ignore when generating the key
Response:

Parameter Type Require Description
BetAmount decimal(16,4) Yes Bet Amount
PayoffAmount decimal(16,4) Yes Payoff Amount
Turnover decimal(16,4) Yes Turnover Amount
Preserve decimal(16,4) Yes Preserve Amount
WagersCount int Yes Bet record count
Currency string Yes Currency code
GameId int No
Game unique id.
Only used for GroupByGame=1.
Error code:

Error Code Message Description
0 Success Success
2 Invalid Key Invalid key
101 Invalid DateTime Invalid time format or start time > end time.
4 (other failures) Other failures
Sample : Please refer to the following time format
StartTime = '2020- 09 - 02T00:00:00';
EndTime = '2020- 09 - 02T23:59:59';

Response samples:

Summarize all games (GroupByGame = 0)
{
"ErrorCode": 0 ,
"Message": "",
"Data": [
{
"BetAmount": 3002.5,
"PayoffAmount": 1.95,
"Turnover": 3002.5,
"Preserve": 0 ,
"WagersCount": 6 ,
"Currency": "THB",
}
}
Count by games
{
"ErrorCode": 0 ,
"Message": "",
"Data": [
{
"BetAmount": 2.5,
"PayoffAmount": 1.95,
"Turnover": 2.5,
"Preserve": 0 ,
"WagersCount": 5 ,
"Currency": "THB",
"GameId": 108
},
{
"BetAmount": 3000 ,
"PayoffAmount": 0 ,
"Turnover": 3000 ,
"Preserve": 0 ,
"WagersCount": 1 ,
"Currency": "THB",
"GameId": 182
}
]
}

Query single game record (deprecated)
URL /GetBetRecordByUuid Method POST Return JSON
Description Querying single bet record by uuid.

Request:

Parameter Type Require Description
WagersId bigint Yes Game record unique id.
Response:

Parameter Type Require Description
Account string Yes Member unique id.
WagersId bigint Yes Game record unique id.
GameId int Yes Game unique id.
WagersTime DateTime Yes Bet time.
BetAmount decimal(16,4) Yes Bet amount.
PayoffTime DateTime No Payoff time.
PayoffAmount decimal(16,4) No Payoff amount.
Status int Yes
Bet Status:
1: Win
2: Lose
SettlementTime DateTime Yes Settlement time.
GameCategoryId int Yes
Game type:
Refer to Chapter 3.1.
Type Int Yes
Statement type:
1: main game
9: free game
11:Reward card
AgentId string Yes Agent unique id
RoundIndex bigint No
RoundIndex of free games of “War Of Dragons” and
“King Kong”
Error code:
Error Code Message Description
0 Success Success
101 Record Not Exist Game record not exist

Query game list
URL /GetGameList Method POST Return JSON
Description Query the information of all games including GameId, name, type, etc.

Response:

Parameter Type Require Description
GameId string Yes Game unique id
Name object Yes
zh-CN：The name of Simplified Chinese
zh-TW：The name of Traditional Chinese.
en-US：The name of English.
GameCategoryId int Yes Game type： see Appendix D
JP boolean Yes
true: this game has in-game JP
false: no in-game JP
Freespin boolean Yes
True as this game supports free spins (§3.2);
False otherwise.
Sorting int No Game page display sorting order
Sample of the request

/GetGameList

AgentId=abcd_THB&Key=0000006b5536a736536e46080b3df80f5cc7aa

Sample of the response body

{
"ErrorCode": 0 ,
"Message": "success",
"Data": [
{
"GameId": 1 ,
"name": {
"en-US": "Royal Fishing",
"zh-CN": "钱龙捕鱼",
"zh-TW": "錢龍捕魚"
},
"GameCategoryId": 5 ,
"JP": false,
"Freespin": false

"Sorting": 1
},
{
"GameId": 2 ,
"name": {
"en-US": "Chin Shi Huang",
"zh-CN": "秦皇传说",
"zh-TW": "秦皇傳說"
},
"GameCategoryId": 1 ,
"JP": false,
"Freespin": true
},
{
"GameId": 4 ,
"name": {
"en-US": "God Of Martial",
"zh-CN": "关云长",
"zh-TW": "關雲長"
},
"GameCategoryId": 1 ,
"JP": false,
"Freespin": false
}
]
}

Query MustHitBy
URL /GetMustHitBy Method POST Return JSON
Description Query information of ‘MustHitBy’

Request:

Parameter Type Require Description
GameId Int No
Game unique id. If not given, return information of all
games.
P.S. please ignore when generating the key.
Response:

Parameter Type Require Description
Currency String Yes Currency code
Game String Yes Game name
GameId Int Yes Game unique id
MustHitByPool Decimal Yes Current pool value of MustHitBy
MustHitByValue Decimal Yes Goal value of MustHitBy
Error code:

Error Code Message Description
0 Success Success
9 Execution Error Execution Error
101 Record Not Exist Record Not Exist
Sample of the request

/GetMustHitBy

AgentId=abcd_THB&Key=000000eb51beeeab91421619241e4d9e6f79a

Sample of the response body

{
"ErrorCode": 0 ,
"Message": "success",
"Data": [
{
"Currency": "THB",

"Game": "CrazySeven",
"GameId": 35 ,
"MustHitByPool": 2459.8625,
"MustHitByValue": 3000
},
{
"Currency ": "THB",
"Game": "Bao boon chin",
"GameId": 36 ,
"MustHitByPool ": 2413. 6871 ,
"MustHitByValue ": 3000
},
{
"Currency ": "THB",
"Game": "Dragon Treasure",
"GameId": 46 ,
"MustHitByPool": 3000 ,
"MustHitByValue": 3000
},
{
"Currency ": "THB",
"Game": "SuperAce",
"GameId": 49 ,
"MustHitByPool": 2937. 4401 ,
"MustHitByValue": 3000
}
]
}

Query member status
URL /GetMemberInfo Method POST Return JSON
Description Check current status of a member including account, usable credits and other information.

Request:

Parameter Type Require Description
Accounts string Yes
Member unique identification value. Optional. Two
differenct mode as following:
Multiple accounts: separated by commas
Single account.
Response:

Parameter Type Require Description
Account string Yes Member unique identification value.
Balance Decimal(16,4) Yes Member wallet balance (0 if the account does not exist)*
Status int Yes
status：
1: online
2: offline
3: account does not exist.

The wallet balance returned is not real-time. There is a few seconds of delay.
Sample of QueryString:
//Query single user
Accounts=Test001&AgentId=abcd_RMB

//Multi-users : Separate with commas
Accounts=Test001,Test002&AgentId=abcd_RMB

Sample of the request

/GetMemberInfo

Accounts=Test001&AgentId=abcd_THB&Key=000000446c647a1b506110747564e7a416efeb000000

Sample of the response body

{
"ErrorCode": 0 ,

"Message": "success",
"Data": [
{
"Account": "Test001",
"Balance": 260 .03,
"Status": 2
}
]
}

3.2. Free Spins
“Free spins” (also known as “free games”, “free rounds”) contains several concepts that are easy to confuse,
which are listed as follows:
➢ Bonus games
Players may randomly get a number of free spins in the regular game. No matter how many spins the
player gets, all the payout amounts of the free spins will be combined with the bet amount and payout
amount of the regular game that triggered the free spins into a single bet request. This bet request has
no difference from a bet request of a regular game, including the endpoint and format. Please refer to
§4.2.3.
The above description does not apply to WAR OF DRAGONS (game ID = 9) 和 MEDUSA (game ID
= 101).

➢ Bonus games of WAR OF DRAGONS (game ID = 9) 和 MEDUSA (game ID = 101)
The bonus games of these two games are different from other games. There will be cases of multiple
bet requests. The format of the bet request is also slightly different from the regular game, please refer
to §4.2.4 Offline payments.

➢ Item card
Players have a chance to get item cards in the game. When used, they will cost some amount and get a
number of free spins. No matter how many spins the player gets, all the payout amounts will be
combined with the bet amount (the cost) into a single bet request. This request has the same format and
endpoint as the regular game, but has a different statementType. Please refer to §4.2.3 and Appendix C

Statement Types.
➢ Buy bonus
Some games allow players to buy bonus games. After purchasing, they can get a number of free spins.
Similar to item cards, no matter how many spins the player gets, all the payout amounts will be
combined with the purchase cost into a single bet request. This request has the same format and
endpoint as the regular game, but has a different statementType. Please refer to §4.2.3 and Appendix C

Statement Types.
➢ Free Spins
The operators are allowed to give free spins to players. The rounds of free spins are used first when the
player enters the game. For more details, please refer to §4.2.4 Free Spins.

The free spins described in this chapter are the last of the above, that is, the free spins that are given to
players by the operators.

Give free spins to a member
URL /CreateFreeSpin Method POST Return JSON
Description Give free spin rounds to a specified member

Request:

Parameter Type Require Description
Account String Yes Member account.
Currency String Yes Currency used by the member.
ReferenceId String Yes
Unique identifier of the free spins given by this request
(50 characters at most).
FreeSpinValidity Date Yes
The date when the given free spins are expired (GMT-4).
Format: YYYY-MM-DD T HH:MM:SS
(2006- 01 - 02 T 15:04:05)
The validity period shall not exceed 31 days from the start
time
NumberOfRounds Int Yes Count of the given free spins.
GameIds String Yes
IDs of games for the given free spins. Comma separated if
more than one.
(200 characters including commas at most)
BetValue Double No
The betting value for the player to use for the free spins.
Minimum bet value is used if this parameter is not given.
P.S. please ignore when generating the key.
StartTime String No
The date when the given free spins can be used (GMT-4).
Format: YYYY-MM-DD T HH:MM:SS
(2006- 01 - 02 T 15:04:05)
If not given, the given free spins can be used immediately.
P.S. please ignore when generating the key.
AllowStop Bool No
Whether the free spins can be aborted before completion.
P.S. please ignore when generating the key.
MaxWin Double No
Maximum accumulated winning limit
If not specified, there is no upper limit.
P.S. please ignore when generating the key.
Response:

Parameter Type Require Description
CreateTime Bigint Yes Timestamp
Error code:

Error Code Message Description
0 Success Success
9 Execution Error Server error
101 Invalid Date Time Format of FreeSpinValidity is not correct
101 Incorrect NumberOfRounds NumberOfRounds is not a valid number
101 Incorrect GamesIds
Some of id(s) in GameIds is invalid or does not
support free spins
101 Too many GameIds GameIds is longer than 200 characters
101 Empty ReferenceId Empty ReferencedId
101 ReferenceId too long ReferencedId is longer than 50 characters
101 Invalid bet value BetValue is not a valid value
102 ReferenceId Exist ReferencedId is used
104 Currency Not Exist The game provider does not support this currency
Sample of the request 1 (json)

/CreateFreeSpin

{
"Account": "test01",
"Currency": "THB",
"ReferenceId": "freespintest0001",
"FreeSpinValidity": " 2023 - 01 - 01T12:00:00",
"NumberOfRounds": 10,
"GameIds": "108,110"
}

Sample of the request 2 (form-urlencoded)

/CreateFreeSpin

Account=test01&Currency=THB&ReferenceId=freespintest0001&FreeSpinValidity= 2023 - 01 - 01T12:00:
00 &NumberOfRounds= 10 &GameIds=108,110&AgentId=abcd_THB&Key=0000006e5fd5af6b15cce4e668c3e47de
5f591000000

Sample of the response body

{
"ErrorCode": 0 ,
"Message": "success",

"CreateTime": 1659693600
}

Query overview of free spins
URL /GetFreeSpinRecordSummary Method POST Return JSON
Description Get summary of bet and send and used records by specific time range

Request:

Parameter Type Require Description
StartTime DateTime Yes Start time
EndTime DateTime Yes End time
Currency string No
Currency code.
If not given, summary BY each currency will be returned.
P.S. please ignore when generating the key.
FilterAgent bool No
Filter records which not belong to the agent
If not given, summary of all agents will be returned.
P.S. please ignore when generating the key.
Response-Result:

Parameter Type Require Description
BetAmount decimal(16,4) Yes Bet Amount (must be 0)
PayoffAmount decimal(16,4) Yes Payoff Amount
WagersCount int Yes Bet record count
Currency string Yes Currency code
WinlossAmount decimal(16,4) Yes Payoff-bet amount difference
Response-Overview:

Parameter Type Require Description
TotalSend int Yes Number of free spins were given
TotalUsed int Yes Number of free spins were used
TotalUnused int Yes Number of free spins were unused
Error code:
Error Code Message Description
0 Success Success
2 Invalid Key Invalid key
101 Invalid DateTime Invalid time format or start time > end time.
4 (other failures) Other failures

Sample of the request

/GetFreeSpinRecordSummary

StartTime= 2023 - 05 - 02 T00:00:00&EndTime= 2023 - 05 - 03 T00:00:00&AgentId=abcd_THB&Key= 000000 517e59
66d1e97e99fec757e71d61add3 000000

Sample of the response body

{
"ErrorCode": 0,
"Message": "",
"Data": {
"Result": [
{
"BetAmount": 0 ,
"PayoffAmount": 0.2,
"WagersCount": 2,
"Currency": "USD",
"WinlossAmount": 0
},
{
"BetAmount": 0 ,
"PayoffAmount": 0.2,
"WagersCount": 4,
"Currency": "THB",
"WinlossAmount": - 3.8
}
],
"Overview": {
"TotalSend": 20,
"TotalUsed": 6,
"TotalUnused": 14
}
}
}

Query the detail of free spins were given
URL /GetFreeSpinSendDetail 2 Method POST Return JSON
Description Get the detail of free spins were given by specific time range

Request:

Parameter Type Require Description
StartTime DateTime Yes Start time
EndTime DateTime Yes End time
Page int Yes Page( start from 1 )
PageLimit int Yes
Number of transaction record per page. Must not more
than 25,000 and not less than 10000.
Response-Result:

Parameter Type Require Description
Account string Yes Member unique id
ReferenceID string Yes Free spin given id
SendAmount int Yes Number of given free spins
SendTime DateTime Yes Time of given free spins
ExpiredTime DateTime Yes Expired time of free spins
UpdateTime DateTime Yes Last updated time for free spins
SendGame string Yes Games of given free spins
UsedAmount int Yes Number of used free spins
UnusedAmount int Yes Number of unused free spins
ClaimGame int Yes Claim game of free spins (0: not claimed to any game)
Response-Pagination:
Element Type Require Description
CurrentPage int Yes Current page.
TotalPages int Yes Total pages.
PageLimit int Yes Number of transaction record per page.
TotalNumber int Yes Total transaction amount.

Error code:
Error Code Message Description
0 Success Success
2 Invalid Key Invalid key

101 Invalid DateTime Invalid time format or start time > end time.
4 (other failures) Other failures
Sample of the request

/GetFreeSpinSendDetail 2

StartTime= 2023 - 05 - 02 T00:00:00&EndTime= 2023 - 05 - 03 T00:00:00&Page= 1 &PageLimit= 25000 &AgentId=ab
cd_THB&Key= 000000 517e5966d1e97e99fec757e71d61add3 000000

Sample of the response body

{
"ErrorCode": 0,
"Message": "",
"Data": {
"Result": [
{
"Account": "test001_THB",
"ReferenceID": "1683016002999",
"SendAmount": 10 ,
"SendTime": "2023- 05 - 02T04:27:10-04:00",
"ExpiredTime": "2023- 06 - 01T00:00:00-04:00",
"UpdateTime": "2023- 05 - 04T08:00:00-04:00",
"SendGame": "134",
"UsedAmount": 4 ,
"UnusedAmount": 6 ,
"ClaimGame": 134
},
{
"Account": "test001_USD",
"ReferenceID": "1683016170598",
"SendAmount": 10 ,
"SendTime": "2023- 05 - 02T04:29:32-04:00",
"ExpiredTime": "2023- 06 - 01T00:00:00-04:00",
"UpdateTime": "2023- 05 - 05T09:10:00-04:00",
"SendGame": "77,78",
"UsedAmount": 2 ,
"UnusedAmount": 8 ,
"ClaimGame": 78

}
],
"Pagination":{
"CurrentPage": 1 ,
"TotalPages": 1 ,
"PageLimit": 25000 ,
"TotalNumber": 2
}
}
}

Query game records of free spins
URL /GetFreeSpinRecordByTime Method POST Return JSON
Description Get free spins game records by specific time range

Request:

Parameter Type Require Description
StartTime DateTime Yes
Start time.
Format: YYYY-MM-DD T hh:mm:ss such as
2021 - 01 - 01 T 03:00:00. GMT-4 should be used.
EndTime DateTime Yes
End time.
Format: the same as StartTime.
P.S. Bet records could possibly be delayed. Please DO
NOT use current time as EndTime. Using the time 5 to
10 minutes ago is recommended.
Page int Yes Page( start from 1 )
PageLimit int Yes
Number of transaction record per page. Must not more
than 20,000 and not less than 10000.
GameId int No
Game unique id.
P.S. please ignore when generating the key.
FilterAgent int No
Filter records which not belong to the agent
If not given, summary of all agents will be returned.
P.S. please ignore when generating the key.
Response-Result:

Parameter Type Require Description
Account string Yes Member unique id
GameId int Yes Game unique id
WagersId bigint Yes Game record unique id
BetAmount decimal(16,4) Yes Bet Amount.*
PayoffAmount decimal(16,4) Yes Payoff Amount
WagersTime DateTime Yes Bet Time
Currency int Yes Currency code
ReferenceId string Yes Free spin given id
Type int Yes
Statement type:
19: free spin
27: spin bonus(bet)
28: spin bonus(win)
BetAmount of a free spin is only a base value used to calculate PayoffAmount. No actual deduction is
made.
Response-Pagination:

Parameter Type Require Description
CurrentPage int Yes Current page.
TotalPages int Yes Total pages.
PageLimit int Yes Number of transaction record per page.
TotalNumber int Yes Total transaction amount.
Error code:

Error Code Message Description
0 Success Success
2 Invalid Key Invalid key
101 Invalid DateTime Invalid time format or start time > end time.
4 (other failures) Other failures
Sample of the request

/GetFreeSpinRecordByTime

StartTime= 2023 - 05 - 02 T00:00:00&EndTime= 2023 - 05 - 03 T00:00:00&Page= 1 &PageLimit= 10000 &AgentId=ab
cd_THB&Key=0000006e5fd5af6b15cce4e668c3e47de5f591000000

Sample of the response body

{
"ErrorCode": 0,
"Message": "",
"Data": {
"Result": [
{
"Account": "test001_THB",
"GameId": 134,
"WagersId": 1681973017020873134,
"BetAmount": - 1,
"PayoffAmount": 0,
"Currency": "THB",
"WagersTime": "2023- 05 - 02T04:27:47-04:00",

"ReferenceId": "1683016002999",
"Type": 19 ,
},
{
"Account": "test001_USD",
"GameId": 78,
"WagersId": 1682472371000077078,
"BetAmount": - 0.1,
"PayoffAmount": 0,
"Currency": "USD",
"WagersTime": "2023- 05 - 02T04:42:35-04:00",
"ReferenceId": "1683016170598",
"Type": 19 ,
},
],
"Pagination": {
"CurrentPage": 1,
"TotalPages": 1,
"PageLimit": 10000,
"TotalNumber": 2
}
}
}

Query free spin usage records(deprecated)
URL /GetFreeSpinDashflow Method POST Return JSON
Description Get usage records of free spins after UpdateTime

Request:

Parameter Type Require Description
UpdateTime DateTime Yes Query time
Response:

Parameter Type Require Description
Account string Yes Member unique id
ReferenceID string Yes Free spin given id
SendTime DateTime Yes Free spin given time
ExpiredTime DateTime Yes Time of given free spins
UpdateTime DateTime Yes Expired time of free spins
SendGame string Yes Games of given free spins
SendAmount int Yes Number of free spins were given
UsedAmount int Yes Number of used free spins
UnusedAmount int Yes Number of unused free spins
ClaimGame int Yes Claim game of free spins (0: not claimed to any game)
Error code:

Error Code Message Description
0 Success Success
2 Invalid Key Invalid key
9 Failure Executing Internal error by the game provider
101 Invalid DateTime Invalid time format or start time > end time.
4 (other failures) Other failures
Sample of the request

/GetFreeSpinDashflow

UpdateTime= 2023 - 11 - 01T00:00:00&AgentId=abcd_RMB&Key=00000009106ae76957acd37776f90e9c6db4780
00000

Sample of the response body

{
"ErrorCode": 0,
"Message": "",
"Data": [
{
"Account": "test1",
"ReferenceID": "testReferenceID_1",
"SendTime": "2023- 11 - 01T02:30:14-04:00",
"ExpiredTime": "2023- 11 - 05T12:00:00-04:00",
"UpdateTime": "2023- 11 - 01T02:30:18.52-04:00",
"SendAmount": 1,
"UsedAmount": 1,
"UnusedAmount": 0,
"ClaimGame": 49
},
{
"Account": "test2",
"ReferenceID": "testReferenceID_2",
"SendTime": "2023- 11 - 01T02:37:58-04:00",
"ExpiredTime": "2023- 11 - 05T12:00:00-04:00",
"UpdateTime": "2023- 11 - 02T02:38:31.93-04:00",
"SendAmount": 10,
"UsedAmount": 8,
"UnusedAmount": 2,
"ClaimGame": 49
}
]
}

Query game records of FreeSpin by ReferenceID
URL /GetFreeSpinRecordByReferenceID Method POST Return JSON
Description Get free spins game records by specific id

Request:

Parameter Type Require Description
ReferenceID string Yes Free spin unique id
Response:

Parameter Type Require Description
Account string Yes Member unique id
GameId int Yes Game unique id
WagersId bigint Yes Game record unique id
BetAmount decimal(16,4) Yes Bet Amount (must be 0)
PayoffAmount decimal(16,4) Yes Payoff Amount
Currency string Yes Currency code
WagersTime DateTime Yes Bet Time
ReferenceId string Yes Free spin unique id
Type int Yes
Statement type:
19: free spin
27: spin bonus(bet)
28: spin bonus(win)
Error code:
Error Code Message Description
0 Success Success
2 Invalid Key Invalid key
9 Execution Error Internal error by the game provider
4 (other failures) Other failures

Sample of the request
/GetFreeSpinRecordByReferenceID

ReferenceID=freespin_referenceId001&AgentId=abcd_THB&Key=000000483147ccfa09067968e6db1a9fae
c20e000000

Sample of the response body

{
"ErrorCode": 0,
"Message": "",
"Data": [
{
"Account": "test01",
"GameId": 49,
"WagersId": 1699349260008306049,
"BetAmount": 0,
"PayoffAmount": 0,
"Currency": "THB",
"WagersTime": "2023- 11 - 16T01:00:00-04:00",
"ReferenceId": "freespin_referenceId001",
"Type": 19 ,
},
{
"Account": "test01",
"GameId": 49,
"WagersId": 1699349260008307049,
"BetAmount": 0,
"PayoffAmount": 1,
"Currency": "THB",
"WagersTime": "2023- 11 - 16T01:00:00-04:00",
"ReferenceId": "freespin_referenceId001",
"Type": 19 ,
}
]
}

Cancel the given rounds of free spin
URL <API URL> /CancelFreeSpin Method POST Return JSON
Description Cancel free spin rounds
Request:

Parameter Type Require Description
ReferenceId String Yes Unique identifier of the free spins
Response:

Parameter Type Require Description
CancelTime Bigint Yes Timestamp
Error code:

Error Code Message Description
0 Success Success
2 Invalid Key Invalid Key
9 Execution Error Server error
101 Free spin not found Free spin is not exist
101 Free spin already expired Free spin is already expired
101
Free spin already canceled or free spin
rounds have been used up
Free spin has already canceled or free spin rounds
have been used up by player
4 (other failures) Other failures
Sample of the request 1 (json)

/CancelFreeSpin

{
"ReferenceId": "freespintest0001",
"AgentId": "abcd_THB",
"Key": "0000006ee9d3d72a696ae6f2fbc2ca40735738000000"
}

Sample of the request 2 (form-urlencoded)

/CancelFreeSpin

ReferenceId=freespintest0001&AgentId=abcd_THB&Key=0000006ee9d3d72a696ae6f2fbc2ca40735738000
000

Sample of the response body

{
"ErrorCode": 0,
"Message": "",
"CancelTime": 1698796800
}

Cancel the player’s rounds of free spin
URL <API URL> /CancelFreeSpinByAccount Method POST Return JSON
Description Cancel the player’s rounds of free spin
Request:

Parameter Type Require Description
Account String Yes Member account
Response:

Parameter Type Require Description
CancelTime Bigint Yes Timestamp
Error code:

Error Code Message Description
0 Success Success
2 Invalid Key Invalid Key
9 Execution Error Server error
14 User not found Member is not exist
101
Free spin already canceled or free spin
rounds have been used up
The player’s free spins have been canceled or have
been used up by player
4 (other failures) Other failures
Sample of the request 1 (json)

/CancelFreeSpinByAccount
{
"Account": "test01",
"AgentId": "abcd_THB",
"Key": "000000183d22571c28ea6e35fc6b90fd21ce29000000"
}

Sample of the request 2 (form-urlencoded)

/CancelFreeSpinByAccount

Account=test01&AgentId=abcd_THB&Key=000000183d22571c28ea6e35fc6b90fd21ce29000000

Sample of the response body

{
"ErrorCode": 0,
"Message": "",
"CancelTime": 1698796800
}

Give free spins to multiple members
URL /CreateFreeSpinForMany Method POST Return JSON
Description Give free spin rounds to specified members

Request:

Parameter Type Require Description
Accounts String Yes
Member account, multiple accounts separated by
commas(up to 200 accounts)
Currency String Yes Currency used by the member.
ReferenceIds String Yes
Unique identifier of the free spins given by this request
(50 characters at most), multiple referenceIds separated by
commas(up to 200 referenceIds)
FreeSpinValidity Date Yes
The date when the given free spins are expired (GMT-4).
Format: YYYY-MM-DD T HH:MM:SS
(2006- 01 - 02 T 15:04:05)
NumberOfRounds Int Yes Count of the given free spins.
GameIds String Yes
IDs of games for the given free spins. Comma separated if
more than one.
(200 characters including commas at most)
BetValue Double No
The betting value for the player to use for the free spins.
Minimum bet value is used if this parameter is not given.
P.S. please ignore when generating the key.
StartTime String No
The date when the given free spins can be used (GMT-4).
Format: YYYY-MM-DD T HH:MM:SS
(2006- 01 - 02 T 15:04:05)
If not given, the given free spins can be used immediately.
P.S. please ignore when generating the key.
Response:

Parameter Type Require Description
CreateTime Bigint Yes Timestamp
FailedAccounts Array string Yes Failed accounts for giving free spin rounds
FailedReferenceIds Array string Yes Failed referenceIds for giving free spin rounds
FailedErrorCodes Array int Yes Error codes for failed referenceIds
FailedMessages Array string Yes Error messages for failed referenceIds
Error code (for overall results i.e. ErrorCode):

Error Code Message Description
0 Success Success
4 Free spin disabled Free spin is disabled for this agent
9 Execution Error Server error
10 Server maintaining The server is under maintenance.
101
Number of accounts and referenceIds not
match
Mismatch between player accounts and referenceIds
101 Too many accounts and referenceIds Too many accounts and referenceIds
103 Partial create free spin failed Partial failure to give free game rounds
Error code (for each failed referenceId i.e. FailedErrorCodes)

Error Code Message Description
4 Free spin quota exceeded The free spin quota is exceeded
9 Execution Error Errors occurred during execution.
101 Invalid Date Time Format of FreeSpinValidity is not correct
101 Incorrect NumberOfRounds NumberOfRounds is not a valid number
101 Incorrect GamesIds
Some of id(s) in GameIds is invalid or does not
support free spins
101 Too many GameIds GameIds is longer than 200 characters
101 Empty ReferenceId Empty ReferencedId
101 ReferenceId too long ReferencedId is longer than 50 characters
102 ReferenceId Exist ReferencedId is used
104 Currency Not Exist The game provider does not support this currency
Sample of the request 1 (json)

/CreateFreeSpinForMany
{
"Accounts": "test01,test02",
"Currency": "THB",
"ReferenceIds": "freespintest0001,freespintest0002",
"FreeSpinValidity": "2023- 01 - 01T12:00:00",
"NumberOfRounds": 10 ,
"GameIds": "108,110",
"StartTime": "2023- 01 - 01T00:00:00",
"AgentId": "abcd_THB",
"Key": "000000ee51bf8a79e62845e7cc4ce22126a32d000000"
}

Sample of the response body (success)

{
"ErrorCode": 0,
"Message": "",
"CreateTime": 1672531200
"FailedAccounts": [],
" FailedReferenceId": [],
"FailedErrorCodes": [],
"FailedMessages": []
}

Sample of the response body (failed for all)

{
"ErrorCode": 4 ,
"Message": "Free spin disable",
"CreateTime": 1672531200
"FailedAccounts": ["test01","test02","test03"],
"FailedReferenceId": ["freespintest0001","freespintest0002","freespintest0003"],
"FailedErrorCodes": [],
"FailedMessages": []
}

Sample of the response body (partially failed)

{
"ErrorCode": 103 ,
"Message": "Partial create free spin failed",
"CreateTime": 1672531200
"FailedAccounts": ["test01"],
"FailedReferenceId": ["freespintest0001","freespintest0003"],
"FailedErrorCodes": [102,4],
"FailedMessages": ["ReferenceId Exist","Free spin quota exceeded"]
}

Query the bet amount for free spins
URL /GetGameBetList Method POST Return JSON
Description Query the bet amount for free spins in particular game

Request:

Parameter Type Require Description
GameId int Yes Game unique identification value
Currency string Yes Currency Code
Response:
Parameter Type Require Description
GameId int Yes Game unique identification value
Currency string Yes Currency Code
BetList array float Yes Free spins bet list

Error code:
Error Code Message Description
0 Success Success
9 Internal Error Server error
101 Invalid game id Invalid game unique identifier value
101 This game does not allow free spin This game does not support free spins.
104 Invalid currency Invalid currency code

Sample of request 1 (json)

/GetGameBetList
{
"GameId": " 49 ",
"Currency": "THB",
"AgentId": "abcd_THB",
"Key": "0000001af5eae255762861415e9c6100e54e08000000"
}

Sample of request 2 (form-urlencoded)

/GetGameBetList

GameId= 49 &Currency=THB&AgentId=abcd_THB&Key=0000001af5eae255762861415e9c6100e54e08000000

Sample of response body

{
"ErrorCode": 0,
"Message": "",
"GameId": 49,
"Currency": "THB",
"BetList": [
1,
2,
3,
5,
10,
20,
30,
40,
50,
80,
100,
200,
500,
1000,
2000,
3000,
4000
]
}

Give spin bonus to a member..........................................................................................................
URL /CreateSpinBonus Method POST Return JSON
Description Give spin bonus rounds to a specified member

Request:

Parameter Type Require Description
Account String Yes Member account.
Currency String Yes Currency used by the member.
ReferenceId String Yes
Unique identifier of the free spins given by this request
(50 characters at most).
FreeSpinValidity Date Yes
The date when the given free spins are expired (GMT-4).
Format: YYYY-MM-DD T HH:MM:SS
(2006- 01 - 02 T 15:04:05)
The validity period shall not exceed 31 days from the start
time
NumberOfRounds Int Yes Count of the given free spins.
GameIds String Yes
IDs of games for the given free spins. Comma separated if
more than one.
(200 characters including commas at most)
Multiplier Int Yes
Wagering requirement: The players must accumulate bets
equal to a certain multiple of the bonus amount before
they can claim the bonus. It can be set starting from 0x ,
with a recommended value of 5x to ensure the
reasonableness of the game
WagerPeriod Int Yes Valid wagering period, in hours.
BetValue Double No
The betting value for the player to use for the free spins.
Minimum bet value is used if this parameter is not given.
P.S. please ignore when generating the key.
StartTime String No
The date when the given free spins can be used (GMT-4).
Format: YYYY-MM-DD T HH:MM:SS
(2006- 01 - 02 T 15:04:05)
If not given, the given free spins can be used immediately.
P.S. please ignore when generating the key.
MinBonus Double No
Minimum bonus; initial bonus amount.
P.S. please ignore when generating the key.
MaxBonus Double No
Maximum cumulative bonus;
No limit on cumulative bonus if not specified.
P.S. please ignore when generating the key.
Response:

Parameter Type Require Description
CreateTime Bigint Yes Timestamp
Error code:

Error Code Message Description
0 Success Success
4 Spin bonus disable No authorization to issue spin bonus.
4 Free spin quota not enough Insufficient quota to issue.
9 Execution Error Server error
101 Invalid Date Time Format of FreeSpinValidity is not correct
101 Incorrect NumberOfRounds NumberOfRounds is not a valid number
101 Incorrect GamesIds
Some of id(s) in GameIds is invalid or does not
support free spins
101 Too many GameIds GameIds is longer than 200 characters
101 Empty ReferenceId Empty ReferencedId
101 ReferenceId too long ReferencedId is longer than 50 characters
101 Invalid bet value BetValue is not a valid value
101 Multiplier less than ReferencedId is used
102 ReferenceId Exist The game provider does not support this currency
104 Currency Not Exist GameIds is longer than 200 characters
Sample of the request 1 (json)

/CreateSpinBonus
{
"Account": "test01",
"Currency": "THB",
"ReferenceId": "spinbonustest0001",
"FreeSpinValidity": " 2023 - 01 - 01T12:00:00",
"NumberOfRounds": 10,
"GameIds": "108,110",
"Multiplier": 5,
"WagerPeriod": 24,
"AgentId": "abcd_THB",
"Key": "0000007d68c7c0fc7f0c1ead7a56af8c593dd0000000"
}

Sample of the request 2 (form-urlencoded)

/CreateSpinBonus
Account=test01&Currency=THB&ReferenceId=spinbonustest0001&FreeSpinValidity= 2023 - 01 - 01T12:00
:00&NumberOfRounds= 10 &GameIds=108,110&Multiplier= 5 &WagerPeriod= 24 &AgentId=abcd_THB&Key= 0000
007d68c7c0fc7f0c1ead7a56af8c593dd0000000

Sample of the response body

{
"ErrorCode": 0,
"Message": "",
"CreateTime": 1716968262
}

4. APIs Provided by the Operator
The operator should provide ‘auth’,‘ bet’, and ‘cancelBet’ at least. Contact the game provider to
confirm the requirements of other APIs.

4.1. API Protocol and Authentication
The operator should provide following information:
⚫ <api_url> API URL root path of the operator

HTTP POST is used for most APIs, even some of them can accept HTTP GET.
JSON format is used to pass parameters if HTTP POST is used.

HTTP request header:
Content-type: application/json

Authentication (optional)
⚫ The operator could ask the game provider to add a credential in the header of each http request.
⚫ See Appendix E for available authentication protocols.
⚫ The authentication is not mandatory.

Response
Responses from the operator should be JSON format.
Each response should have following columns:

Parameter Type Require Description
errorCode int Yes
API status code
0 : success
Others: defined by each API
message strint No API error message. Not necessary if the request succeeded.
4.2. APIs
Generate the Token
⚫ The operator should generate and hold tokens for the players. The operator should pass the token to the
game provider when sending Login or LoginWithoutRedirect requests to the game provider.
⚫ Authentication and bet requests from the game provider carry the token.
⚫ Tokens are used to identify players by the operator.
⚫ The token should not be longer than 800 characters.

Hint: UUID, MD5 or any algorithm which can generate unique string can be considered to generate tokens.
Expired time of tokens is decided by the operator.

Player Authentication
URL /auth Method POST Return JSON
Description Validate the player’s token

Request:

Parameter Type Require Description
reqId string Yes Request unique ID (50 characters at most)
token string Yes Authorized key for requests (800 characters at most)
Response:
Parameter Type Require Description
username string Yes The player’s account
currency string Yes Currency code of the player’s balance (see Appendix B)
balance double Yes Amount of the player’s balance

token string No
New token for next request. Only when the operator
change the token
Error code:
Error Code Message Description
0 Success Success
4 Token expired The token is expired or invalid
5 Other error Other errors; see message for detail
Smple

Post Body

{
"reqId": "0af0c835-c37b-5da0-9e4e-25463e6ed14d"
"token": "6f6d63331c1173c8367e43b5fe6c49dd"
}
Response

{
"errorCode": 0 ,
"message": "success",
"username": "testUser",
"currency": "USD",
"balance": 1000 ,
"token": "6f6d63331c1173c8367e43b5fe6c49dd"
}

Player Bet (place bet and settlement together)
The ‘bet’ described in this section is used for slot games and fishing games. See §4.2.7 for card games
(poker) and casino games.
URL /bet Method POST Return JSON

Description

Send a player’s bet to the operator. The settlement is included in this request.
If no response from the operator due to network or other issues, the game provider will either:
cancel this bet (see §4.2.5);
Or retry this bet (see §4.2.6).
The cancellation will proceed by default. The operator can ask the game provider to retry the bet
request, however, the cancellation will be sent after reaching the maximum number of retrying.
The operator and the game provider should determine which action beforehand.
P.S. Offline payments are allowed in some games. The column ‘isFreeRound’ of these bets
should be true and ‘userId’ is used to identify the players. (see §4.2.4)
To process the bet request, use following formula:

If Balance before bet >= betAmount then
Balance after bet = Balance before bet – betAmount + winloseAmount
Else
The bet request fails.

Request:

Parameter Type Require Description
reqId string Yes
Request correlation ID. Has a different value if the request
is resent. (50 characters at most)
token string Yes Authorized key for requests
currency string Yes Currency code of the bet
game int Yes Game unique ID
round (*) bigint Yes Game record unique ID (the same as WagersId in §3.1.3)
wagersTime bigint Yes Bet time
betAmount double Yes Bet amount
winloseAmount double Yes Payoff amount
isFreeRound bool No
true: offline payments (see §4.2.4)
false: otherwise
userId string No
Player unique ID (by the operator’s special demands;
always appears in offline payments )
transactionId bigint No
Wagers id of fishing (by the operator’s special
demands) or 2. Trigger round id of offline payments
platform string No Platform information (by the operator’s special demands;
should be given by the operator of LoginWithoutRedirect
§2.1.1)
statementType int No
statement type (by the operator’s special demands; see
Appendix C)
gameCategory int No
Game category (by the operator’s special demands; see
Appendix D)
freeSpinData object No Free spin information. See Free Spins.
smResult string No Slot machines reporting (for Portugal regulated market)

The ‘round’ parameter is the unique identifier of the player bet. It is also used to identify the cancelling.
Response:

Parameter Type Require Description
username string Yes Player unique ID
currency string Yes Currency code of the player’s balance
balance double Yes Amount of the player’s balance
txId bigint No
Transaction unique ID of the operator (only after the
operator’s recognition)
token string No
New token for next request. Only when the operator
change the token
Error code:
Error Code Message Description
0 Success Success
1 Already accepted The bet is already accepted
2 Not enough balance Not enough balance to bet
3 Invalid parameter Invalid parameters; see message for detail
4 Token expired The token is expired or invalid
5 Other error Other errors; see message for detail

Sample

Post Body

/bet
{
"reqId": "9177b749-cf37-585b-b17c-cfd5024ca6e2",
"token": "6f6d63331c1173c8367e43b5fe6c49dd",
"currency": "USD",
"game": 1 ,
"round": 17238050501001102002 ,

"wagersTime": 1592559162 ,
"betAmount": 10 ,
"winloseAmount": 5
}

Response

{
"errorCode": 0 ,
"message": "success",
"username": "testUser",
"currency": "USD",
"balance": 995 ,
"txId": 108430126 ,
"token": "6f6d63331c1173c8367e43b5fe6c49dd"
}

Special Bets
Special bets are the bets (§4.2.3) with special parameters. /bet is also used.

Offline payments
Relative parameters: isFreeRound, userId, transactionId

Occurred in few games. Since there is no token of an offline player, the token of the latest login is used and
the ‘userId’ column is used to identifying the player. The ‘isFreeRound’ column of such a bet should be true.
The ‘transactionId’ column indicates to the round that triggers this free round.

Here are the games using offline payments:
WARS OF DRAGONS (game ID=9): only free spins.
MEDUSA (game ID = 101): only free spins.
A trigger round could have multiple offline payments. Each of these offline payments has its own ‘round’
and shares the same ‘transactionId’.
P.S. The request of an offline payment will been resend until successful or 10 times retry if timed out or met
other errors. If the operator does not want resend, tell the game provider to configure it. Thus a failed offline
payment will be cancelled as a normal bet.

Example Post Body

{
"reqId": "9177b749-cf37-585b-b17c-cfd5024ca6e2",
"token": "6f6d63331c1173c8367e43b5fe6c49dd",
"currency": "USD",
"game": 9 ,
"round": 17238050501001102002 ,
"wagersTime": 1592559162 ,
"betAmount": 0 ,
"winloseAmount": 55 ,
"userId": " 33 68799_26 79638 ",
"isFreeRound": true,
"transactionId": 1630891368000155009
}

Free Spins
Relative parameters: freeSpinData
This mechanism is enabled or disabled by the operator’s demand. The operator is able to use
CreateFreeSpin (see §3.2.1) to give free spins to a specified member in some games.
⚫ The rounds of the free spin (by referenceId) are bound to the game when the member enters it and
no longer used in other games.
⚫ If there are more than one referenceIds can be bound, which are expired earlier is bound.
⚫ The expiration of the free spins is checked when the member enters the game. That means the
rounds can be used even they are expired before the member leaves the game.
⚫ Free spin rounds are used before normal bets.
⚫ A free spin bet has 0 bet amount.
⚫ The game provider should retry sending a failed free spin bet request or cancel it, which is
determined by the operator. The game provider will retry 10 times at most.
There is an additional parameter, freeSpinData, in the bet requests of free spins as the following format:
Parameter Type Require Description
referenceId string Yes
Unique identifier of the free spins given by the operator’s
request in CreateFreeSpin
remain int Yes Remaining rounds of free spins (only current referenceId).
originalBet float Yes The original bet amount (no actual deduction)
deduct int Yes The number of free spin rounds deducted
skipRidValidation bool No
Indicates whether to skip free spin referenceId validation.
For joint promotions, free spins and their referenceId may
be issued by the game provider, in which case the operator
system must skip referenceId validation.
Sample of request body

/bet

{
"reqId": "9177b749-cf37-585b-b17c-cfd5024ca6e2",
"token": "6f6d63331c1173c8367e43b5fe6c49dd",
"currency": "THB",
"game": 110 ,
"round": 17238050501001102002 ,

"wagersTime": 1592559162 ,
"betAmount": 0 ,
"winloseAmount": 55 ,
"freeSpinData": {
"referenceId": "freespintest0001",
“remain”: 9 ,
"originalBet": 0.5,
“deduct”: 1 ,
}
}

P.S.
Free spins use /bet in general as the above. If the operator demands to separate to place the bet and the
settlement, /sessopmBet (§4.2.7) is used for free spins.

Sample of request body to place the bet of a free spin:
/sessionBet

{
"reqId": "6e6a5dfa-6cd4-4a33-a2b3-78814a0ac024",
"token": "4bd968261627be1d9e52864291db6073",
"currency": "THB",
"game": 142 ,
"round": 2703216731000762142 ,
"wagersTime": 1703762005 ,
"betAmount": 0 ,
"winloseAmount": 0 ,
"userId": "peterweng_su",
"freeSpinData": {
"referenceId": "1703761975259658",
"remain": 4
"originalBet": 1 ,
"deduct": 2
},
"sessionId": 1703216731000762142 ,
"type": 1 ,
"turnover": 0 ,
"preserve": 0
}

Sample of request body to settle a free spin:
/sessionBet

{
"reqId": "12800cdb-dfa7-40c9-ac58-79def977a506",
"token": "4bd968261627be1d9e52864291db6073",
"currency": "THB",
"game": 142 ,
"round": 1703216731000762142 ,
"wagersTime": 1703762005 ,
"betAmount": 0 ,
"winloseAmount": 1.5,
"userId": "peterweng_su",
"freeSpinData": {
"referenceId": "1703761975259658",
"remain": 4 ,
"originalBet": 0 ,
"deduct": 0,
},
"sessionId": 1703216731000762142 ,
"type": 2 ,
"turnover": 0 ,
"preserve": 0
}

Cancel Bet (rollback the bet and settlement)
The ‘cancelBet’ described in this section is used for slot games and fishing games. See §4.2.8 for card
games (poker) and casino games.
URL /cancelBet Method POST Return JSON

Description

Cancel a bet. The bet amount should be returned to the player while the win amount
should be deducted.
The game provider should send continuously until the operator responses. This request can be
sent when the player is offline. The operator could use either userId or token to recognize the
player.
To process a cancel bet request, use following formula:
Balance after cancellation = Balance before cancellation + betAmount – winloseAmount

※ Balance after cancellation should not be negative.
※ If the player’s balance is not enough to process the cancellation, error code 6 should be returned.

Request:

Parameter Type Require Description
reqId string Yes
Request correlation ID. Has a different value if the reqeust
is resent. (50 characters at most)
currency string Yes Currency code of the bet
game int Yes Game unique ID
round (*) bigint Yes Game record unique ID (the same as ‘round’ in §4.2.3)
betAmount double Yes Bet amount
winloseAmount double Yes Payoff amount
userId string Yes Player unique ID
token string Yes The token used for this bet

The ‘round’ parameter is the unique identifier of the player bet. It is also used to identify the cancelling.
Response:

Parameter Type Require Description
username string Yes Player unique ID
currency string Yes Currency code of the player’s balance
balance double Yes Amount of the player’s balance
txId bigint No
Transaction unique ID of the operator (only after the
operator’s cancel)
Error code:

Error Code Message Description
0 Success Success
1 Already canceled The bet is already cancelled
2 Round not found Round not found
3 Invalid parameter Invalid parameters; see message for detail
5 Other error Other errors; see message for detail
6 Cancel refused The bet is already accepted and cannot be cancelled
Sample of Request Post Body

/cancelBet
{
"reqId": "9177b749-cf37-585b-b17c-cfd5024ca6e2",
"currency": "USD",
"game": 1 ,
"round": 17238050501001102002 ,
"betAmount": 10 ,
"winloseAmount": 5 ,
"userId": " 33 68799_26 79638 ",
"token": "6f6d63331c1173c8367e43b5fe6c49dd",
}

Response

{
"errorCode": 0 ,
"message": "success",
"username": "testUser",
"currency": "USD",
"balance": 1000 ,
"txId": 108430126
}

Resend Bet
Several reasons cause no response from the operator, For example, network delay could cause timeout of the
bet and the connection could fail due to packet loss. The game provider can resend such bets if the operator allows.
Resending bets follows the rules:

If still no response from the operator, the game provider can retry the sending. Including the first sending,
a bet could be sent at almost 3 times. The operator can determine how many times to retry;
If still no response after all retries, the game provider should cancel the bet. See §4.2.5.
When the operator receives a bet which was accepted yet, the error code of the response to the game
provider could be either 0 or 1, while 0 means success and 1 means the bet was already accepted, which
are defined in §4.2.3; whatever the error code is, the response must include current balance of the player.
Response

{
"errorCode": 1 ,
"message": "already accepted",
"username": "testUser",
"currency": "USD",
"balance": 995 ,
"txId": 108430126 ,
"token": "6f6d63331c1173c8367e43b5fe6c49dd"
}

Sessional Bet (place bet and settle separately)
For table games such as poker cards, roulettes and bingo games, some allow multiple players play
together while the others allow only player. In any case each player has a unique round number ( sessionId )
than others even they are playing in the same game round; a player might have multiple bets in a game
round while there is one and only one settlement. Each bet or settlement has a unique transaction ID ( round ).

➢ Please note that sessionId is used to represent the round number, and round acts as the transaction
ID rather than the round number.
Game Table
Player A
SessionId #1110001
Round #234002 (Bet)
Round #234004 (Bet)
Round #234007 (Settle)
Player B
SessionId #1110003
Round #986004 (Bet)
Round #986005 (Bet)
Round #986009 (Settle)
SessionId #1110002
Round #517010 (Bet)
Round #517011 (Bet)
Round #517019 (Settle)
Player C
Game
Provider
Bet
{"token":"token_player_a","sessionId": 111001 ,
"round":23004,"type":1}
Operator
Settle
{"token":"token_player_a","sessionId": 111001 ,
"round":23007,"type":2}
URL <API URL>/sessionBet Method POST Return JSON
Description

Send a sessional bet or settlement to the operator, which is used in poker with ‘Bet’ and ‘Settle’.
If no response from the operator due to network or other issues, the game provider has following
choices to do:
Before settling: cancel currency bet, finish and settle the session.
After settling: keep trying sending payment to the operator until the n’th resending (10
times as default). If the sending still failed, the game provider should notify the
operator.
See §4.2.8 for cancelling a sessional bet.
P.S. Because settlement could happen when offline, The column ‘userId’ can be used to identify
the players. An alternative way is to use the offline mode.
Request:

Parameter Type Require Description
reqId string Yes
Request correlation ID. Has a different value if the bet is
resent. (50 characters at most)
token string Yes Authorized key for requests
currency string Yes Currency code of the bet
game int Yes Game unique ID
round (*) bigint Yes Action unique ID of bet/settle such as the transaction ID
offline boolean No Offline status indicator; see in Offline mode.
wagersTime bigint Yes Bet time
betAmount double Yes Bet amount
winloseAmount double Yes Payoff amount
sessionId (**) bigint Yes Game record unique ID (the same as WagersId in §3.1.3)
type int Yes
1 = Bet
2 = Settle
userId string No
Player unique ID. Mandatory for type= 2 ; by the operator’s
special demands for type= 1 )
turnover double Yes
Turnover amount (see the section Turnover (effective bet
amount))
preserve double Yes
Preserve balance (see the section Preserve (pre-deducted
deposit amount))
platform string No
Platform information (by the operator’s special demands;
should be given by the operator of LoginWithoutRedirect
§2.1.1)
sessionTotalBet double No
Bet amount of the whole session (by the operator’s special
demands; only used for the settle)
statementType int No
statement type (by the operator’s special demands; see
Appendix C)
gameCategory int No
Game category (by the operator’s special demands; see
Appendix D)
freeSpinData object No Free spin information. See Free Spins and examples.
smResult string No Slot machines reporting (for Portugal regulated market)

The “round’ parameter is the unique identifier of the bet/settle action. It is also used to identify the
cancelling.
** The ‘sessionId’ parameter is the unique identifier of the whole round including bet(s) and settle. All bet(s)
and settle share the same sessionId.
There are some differences between the games which preserve is used and those do not use preserve.
◆ No preserve :
Bet: preserve = 0, betAmount > 0, winloseAmount = 0
➢ Balance after bet = balance before bet – betAmount
Settle: preserve = 0, betAmount = 0, winloseAmount >= 0
➢ Balance after settle = Balance before settle + winloseAmount

◆ With preserve :
Bet: preserve > 0, betAmount = 0, winloseAmount = 0
➢ Balance after bet = balance before bet – preserve
Settle: preserve > 0, betAmount >= 0, winloseAmount >= 0
Balance after settle = Balance before settle + preserve – betAmount + winloseAmount

Response:

Parameter Type Require Description
username string Yes Player unique ID
currency string Yes Currency code of the player’s balance
balance double Yes Amount of the player’s balance
txId bigint No
Transaction unique ID of the operator (only after the
operator’s recognition)
token string No
New token for next request. Only when the operator
change the token
Error code:

Error Code Message Description
0 Success Success
1 Already accepted The bet is already accepted
2 Not enough balance Not enough balance to bet
3 Invalid parameter Invalid parameters; see message for detail
4 Token expired The token is expired or invalid
5 Other error Other errors; see message for detail
Samples:

Request Post Body (bet without preserve )
/sessionBet
{
"reqId": "b682cf4c-4de8-433c-92aa-8c03f7daf002",
"token": "6f6d63331c1173c8367e43b5fe6c49dd",
"currency": "INR",
"game": 72 ,
"round": 1709179916462815072 ,
"wagersTime": 1714107576 ,
"betAmount": 10 ,
"winloseAmount": 0 ,
"sessionId": 1709179916462705072 ,
"type": 1 ,
"preserve": 0
}

Request Post Body (settle without preserve )
/sessionBet
{
"reqId": "d8729e34-36c7- 4750 - 87c1-0d0283f7ace7",
"token": "6f6d63331c1173c8367e43b5fe6c49dd",
"currency": "INR",
"game": 72 ,
"round": 1709179916462915072 ,
"wagersTime": 1714107599 ,
"betAmount": 0 ,
"winloseAmount": 55 ,
"sessionId": 1709179916462705072 ,
"type": 2 ,
"turnover": 22 ,

"preserve": 0
}

Request Post Body (bet with preserve )
/sessionBet
{
"reqId": "e4034252-86ca-40dc-9e29-8a9beb24f28c",
"token": "ae97a7179a4bc47a99c753704a340f82",
"currency": "THB",
"game": 94 ,
"round": 1654662770005413094 ,
"wagersTime": 1655192382 ,
"betAmount": 0 ,
"winloseAmount": 0 ,
"sessionId": 1654662770005303094 ,
"type": 1 ,
"preserve": 12800
}

Request Post Body (settle with preserve )
/sessionBet
{
"reqId": "63b3e8ba-53fe-48e6-b2c3-ac218b89a1c7",
"token": "ae97a7179a4bc47a99c753704a340f82",
"currency": "THB",
"game": 94 ,
"round": 1654662770005513094 ,
"wagersTime": 1655192471 ,
"betAmount": 912 ,
"winloseAmount": 18240 ,
"sessionId": 1654662770005303094 ,
"type": 2 ,
"turnover": 912 ,
"preserve": 12800
}

Response
{
"errorCode": 0 ,
"message": "success",
"username": "testUser",
"currency": "USD",
"balance": 995 ,
"txId": 108430126
"token": "6f6d63331c1173c8367e43b5fe6c49dd"
}

Turnover (effective bet amount)
If the operator does not give rebates to the player by the betting amount, turnover can be ignored.
Turnover does not mean the betting amount of the game round –– although this value is usually
identical to the summary of the player’s betAmount in most games. If the operator gives the player a rebate
at a certain rate based on the player’s betting amount, turnover is recommended to replace betAmount as the
basement to calculate the rebate.
Consider the case of a dice game the player can bet both SMALL and BIG in which, and the payment is
double of both sides. If the player always bets 100 to BIG and another 100 to SMALL, not only 200 is paid
as the winning in each round but the rebate is also given by the operator.
The player can always bet 200 and get 210 back!
Small
4 - 10
(^100) x2 100

Big
11 - 17
x2
Bet 100

Operator
Player (^) Rebate 5 (5% of the bet)

100 100
Win
Operator
Player (^) Rebate 10 (5% of the bet)
Bet 200
Win 200

To prevent such arbitrage, we provide a different formula of turnover for these games.
𝑡𝑢𝑟𝑛𝑜𝑣𝑒𝑟 = min(𝑏𝑒𝑡𝐴𝑚𝑜𝑢𝑛𝑡, |𝑤𝑖𝑛𝑙𝑜𝑠𝑒𝐴𝑚𝑜𝑢𝑛𝑡 − 𝑏𝑒𝑡𝐴𝑚𝑜𝑢𝑛𝑡|)
Applying this formula to the above case, turnover = min(200, |200-200|) = 0。If the operator uses
turnover to calculate the rebate, 0 is given in this case.

Preserve (pre-deducted deposit amount)
Some gams such as Rummy calculate betAmount at the settle. If the bet is sent to the operator at the end
of the round, the player can withdraw all balance from the operator and fail the settle to avoid the losing as
following:

Win 200
Turnover 0
Operator
Player (^) Rebate 0 (5% of the turnover)
Bet 200
Game round starts
Withdraw all balance
Send bet
Bet fails
Game round fails (balance^ not^ enough)^
Player Game Provider Operator

To prevent such arbitrage, the pre-deducted deposit amount as known as preserve is proposed. The
operator should deduct the preserve amount from the player before the game round starts and return it after

deducting the betting amount to the player at the end. Such process ensures that each game round can be

settled successfully.

Please note that the game provider will verify the player’s balance in the response of the bet request. If
the balance is the same as that at the beginning, the preserve mechanism is thought not implemented
correctly by the operator and the game provider will fail the game round to prevent other potential errors.

Send bet
(with preserve )
Game round starts Bet^ succeeds^
( preserve deducted)
Withdraw all balance (does not affect the preserve)
Send settlement
(return preserve , deduct
bet, pay winning)
Game round ends
successfully
Settlement succeeds
Player Game Provider Operator

Send bet
(with preserve )
Game round fails
Bet succeeds
(but preserve is not
deducted)
Player Game Provider Operator

Cancel Sessional Bet (rollback the bet)...........................................................................................
URL <API URL>/cancelSessionBet Method POST Return JSON
Description

Cancel a sessional bet.
The game provider should send continuously until the operator responses. This request can be
sent when the player is offline. The operator could use either userId or token to recognize the
player.
Request:

Parameter Type Require Description
reqId string Yes
Request correlation ID. Has a different value if the bet is
resent. (50 characters at most)
currency string Yes Currency code of the bet
game int Yes Game unique ID
round (*) bigint Yes Action unique ID of the bet (the same as ‘round’ in §4.2.7)
offline boolean No Offline status indicator; see in Offline mode.
betAmount double Yes
Bet amount
Type = 1: bet amount of that bet request
winloseAmount double Yes Payoff amount. Always 0 in the cancelSessionBet request.
userId string Yes* Player unique ID
token string Yes The token used for this bet or an offline token
sessionId bigint Yes Game record unique ID (the same as ‘sessionId’ in §4.2.7)
type int Yes 1 = Bet
preserve double No Preserve value (the same as ‘preserve’ in §4.2.7)

The “round’ parameter is the unique identifier of the bet/settle action. It is also used to identify the
cancelling.
The ‘userId’ is not used if the offline mode is used.
To process a cancelSessionBet request, use following formula:
◆ No preserve :
➢ Balance after cancel = balance before cancel + betAmount

◆ With preserve :
➢ Balance after cancel = balance before cancel + preserve
Response:

Parameter Type Require Description
username string Yes Player unique ID
currency string Yes Currency code of the player’s balance
balance double Yes Amount of the player’s balance
txId bigint No
Transaction unique ID of the operator (only after the
operator’s cancel)
Error code:

Error Code Message Description
0 Success Success
1 Already canceled The bet is already cancelled
2 Round not found Round not found
3 Invalid parameter Invalid parameters; see message for detail
5 Other error Other errors; see message for detail
P.S. A type-1 sessional bet will always following a previous successful bet. After all bets succeeded or one
of them failed, the session is settled.
⚫ Cancel a type-1 sessional bet: cancel one bet and do not affect other bets in the same session. Only used
for the last bet before settling.
◼ A settlement is acceptable by the operator but a bet is not after the cancelling.
◼ However, the operator could receive the cancel before the bet due to network or other issues.
When the operator receive a bet never happens of the session, the session should be pointed out
any bet of which should be refused.
◼ A type-1 cancelling could be received after the settlement due to network or other issues. In this
case, the game provider calculates the settlement based on the failure of the last bet, so the
operator MUST cancel this bet.
⚫ The settlement (type=2) should never be cancelled.

Appendix A – Language Codes
Language Code
Bengali bn-IN
Danish da-DK
German de-DE
English en-US
Spanish es-AR
French fr-FR
Greek gr-GR
Hindi hi-IN
Indonesian id-ID
Italian It-IT
Japanese ja-JP
Korean ko-KR
Malay ms-MY
Myanmar my-MM
Dutch nl-NL
Portuguese pt-BR
Romanian ro-RO
Russian ru-RU
Swedish sv-SE
Tamil ta-IN
Thai th-TH
Turkish tr-TR
Vietnamese vi-VN
Simplified Chinese zh-CN

Appendix B – Currency Codes
Please refer https://storage.googleapis.com/winbet-tada-cdn-asia/api-documents/Currency-List.xlsx

Appendix C – Statement Types
Code Type
1 Normal bet
9 Offline payment (see §4.2.4)
11 Item card
12 Buy bonus
17 MustHitBy (bet)
18 MustHitBy (win)
19 Free spin
28 Spin Bonus
33 Jackpot Legend Mini
34 Jackpot Legend Minor
35 Jackpot Legend Major
36 Jackpot Legend Grand
Appendix D – Game Categories
Code Category
1 Slot
2 Poker
3 Lobby
5 Fishing
8 Casino (including bingo)
Appendix E – Extra Authentications
Available HTTP authentication protocols are listed in this section.

HTTP Basic Authentication
HTTP Basic Authentication is a method for an HTTP user agent (i.e. the operator defined in this document),
a user name and password when making a request, where credentials is the Base64 encoding of ID and
password jiined by a single colon. Please refer to Wikipedia for more information.

For example:

⚫ username:abc, password:abc123
⚫ abc:abc123

⚫ Base64 encode: YWJjOmFiYzEyMw==
⚫ HTTP request header:
Authorization: Basic YWJjOmFiYzEyMw==

A complete ‘auth’ reqeust (§4.2.2) is listed as following:
Body:
Authorization: Basic YWJjOmFiYzEyMw==
Content-Type: application/json

Body:
{"reqId":"011d3624-90cd-477b-bf05-b8b2c623ee45","token":"dc7b7f79187bbc17cc2994965a736a9c"}

Offline mode (optional)
A settlement (/sessionBet with type=2) or a refund (/cancelSession) could be sent when the token use by the
bet is expired. The operator can demand the game provider use the offline mode. The offline mode is
disabled defaultly. In this mode, the offline indicator is carried as a true value and the offline token is used.
An offline token key is given in advance.
An offline token is created using following algorithm:

SHA224( + + + ‘_’ + )

For example, when the offline token key is given as AAAA-BBBB-CCCC-DDDD, an offline settlement for
round= 26727840008124608 , sessionId= 26727838908124090 and userId=APLAYER, the offline
token is

SHA224(AAAA-BBBB-CCCC-DDDD 2672784000812460826727838908124090 _APLAYER) =
1cb22d550f2d7e755631435c28b9a08b08519f49f6fba46095f755b6

Thus the following request body is sent:
{
"reqId": "0d8098b1-1ee2-47cb-b159-9149e2fb945b",
"token": "1cb22d550f2d7e755631435c28b9a08b08519f49f6fba46095f755b6",
"currency": "USD",
"game": 124 ,
"round": 26727840008124608 ,
"offline": true,
"wagersTime": 1687348800,
"betAmount": 0 ,
"winloseAmount": 0,
"sessionId": 26727838908124090,
"type": 2,
"turnover": 60
}
Please note the offline field is set to true and userId is not used in the offline request.

Appendix F – Testing Tools
The testing tools are provided by the game provider, allowing operator to test the operator-provided APIs
(§4.2). Provides the ability to query samples and call the actual operator API. This testing tools can be
performed in a test environment only.

⚫ API URL root path of the game provider

Each response contains following parameters:

Parameter Type Description
ErrorCode int Status code of the response
Message string Status description of the response
Data Object Response data
Data contains following parameters:

Parameter Type Description
Request Header Object Header of the transmitted HTTP request
[Authorization] HTTP
Basic Authentication
Object Example of HTTP Authentication
Request Body Object HTTP request sent by the game provider
Response Object HTTP response returned by the operator-provided API
{
"Request Header": {
"Content-type": "application/json",
"(Optional) Authorization": "Basic ZGVtbzpwQDU1dzByZA=="
},
"[Authorization] HTTP Basic Authentication": {
"Format": "username:password",
"Encoding": "Base64 encoded",
"Sample": "demo:p@55w0rd",
"Sample Encoded String": "ZGVtbzpwQDU1dzByZA=="
},
}

1. Query Samples
Query the sample requests and responses for each API for reference only, not an actual request being sent.

URL /sample/auth Method GET Return JSON
Description Query auth API sample

Request:

Parameter Type Require Description
Token string No
Authorized key for requests (800 characters at most)
Display sample Token if not provided.
{
"Request Body": {
"reqId": "0af0c835-c37b-5da0-9e4e-25463e6ed14d",
"token": "{Player's Token}"
},
"Response": {
"errorCode": 0,
"message": "success",
"username": "{Player's Username}",
"currency": "{Player's Currency}",
"balance": 1000,
"token": "{Player's Token}"
}
}

URL /sample/bet Method GET Return JSON
Description Query bet API sample

Request:

Parameter Type Require Description
Token string No
Authorized key for requests (800 characters at most)
Display sample Token if not provided.
IsFreeRound bool No True: display sample for offline payments
{
"Request Body": {
"reqId": "9177b749-cf37-585b-b17c-cfd5024ca6e2",
"token": "{Player's Token}",
"currency": "{Player's Currency}",
"game": 9,
"round": 1723805050100110200,

"wagersTime": 1592559162,
"betAmount": 10,
"winloseAmount": 5,
"isFreeRound": true,
"userId": "{Player's UserID}",
"transactionId": 1630891368000155009
},
"Response": {
"errorCode": 0,
"message": "success",
"username": "{Player's Username}",
"currency": "{Player's Currency}",
"balance": 1000,
"txId": 108430126,
"token": "{Player's Token}"
}
}

URL /sample/cancelBet Method GET Return JSON
Description Query cancelBet API sample

Request:

Parameter Type Require Description
Token string No
Authorized key for requests (800 characters at most)
Display sample Token if not provided.
IsFreeRound bool No True: display sample for offline payments
{
"Request Body": {
"reqId": "e4034252-86ca-40dc-9e29-8a9beb24f28c",
"currency": "{Player's Currency}",
"game": 9,
"round": 1723805050100110200,
"betAmount": 10,
"winloseAmount": 5,
"userId": "{Player's User ID}",
"token": "{Player's Token}"
},
"[Bet Request Body]": {
"reqId": "9177b749-cf37-585b-b17c-cfd5024ca6e2",

"token": "{Player's Token}",
"currency": "{Player's Currency}",
"game": 9,
"round": 1723805050100110200,
"wagersTime": 1592559162,
"betAmount": 10,
"winloseAmount": 5,
"isFreeRound": true,
"userId": "{Player's UserID}",
"transactionId": 1630891368000155009
},
"Response": {
"errorCode": 0,
"message": "success",
"username": "{Player's Username}",
"currency": "{Player's Currency}",
"balance": 1000,
"txId": 108430126,
"token": "{Player's Token}"
}
}

URL /sample/sessionBet Method GET Return JSON
Description Query sessionBet API sample

Request:

Parameter Type Require Description
Token string No
Authorized key for requests (800 characters at most)
Display sample Token if not provided.
Type int No
Bet type:
1 = Bet
2 = Settle
Display bet sample if not provided
Preserve double No Preserve balance
{
"Request Body": {
"reqId": "e4034252-86ca-40dc-9e29-8a9beb24f28c",
"token": "{Player's Token}",
"currency": "{Player's Currency}",

"game": 94,
"round": 1654662770005413094,
"wagersTime": 1655192382,
"betAmount": 100,
"winloseAmount": 0,
"sessionId": 1654662770005303094,
"type": 1,
"userId": "{Player's UserID}",
"turnover": 0,
"preserve": 1000
},
"Response": {
"errorCode": 0,
"message": "success",
"username": "{Player's Username}",
"currency": "{Player's Currency}",
"balance": 1000,
"txId": 108430126,
"token": "{Player's Token}"
}
}

URL /sample/cancelSessionBet Method GET Return JSON
Description Query cancelSessionBet API sample

Request:

Parameter Type Require Description
Token string No
Authorized key for requests (800 characters at most)
Display sample Token if not provided.
Preserve double No Preserve balance
{
"Request Body": {
"reqId": "9177b749-cf37-585b-b17c-cfd5024ca6e2",
"currency": "{Player's Currency}",
"game": 94,
"round": 1654662770005413094,
"betAmount": 0,
"winloseAmount": 0,
"userId": "{Player's User ID}",

"token": "{Player's Token}",
"sessionId": 1654662770005303094,
"type": 1,
"preserve": 1000
},
"[Session Bet Request Body]": {
"reqId": "e4034252-86ca-40dc-9e29-8a9beb24f28c",
"token": "{Player's Token}",
"currency": "{Player's Currency}",
"game": 94,
"round": 1654662770005413094,
"wagersTime": 1655192382,
"betAmount": 0,
"winloseAmount": 0,
"sessionId": 1654662770005303094,
"type": 1,
"userId": "{Player's UserID}",
"turnover": 0,
"preserve": 1000
},
"Response": {
"errorCode": 0,
"message": "success",
"username": "{Player's Username}",
"currency": "{Player's Currency}",
"balance": 1000,
"txId": 108430126,
"token": "{Player's Token}"
}
}

2. Actually calling the operator-provided API
Call the operator-provided APIs and send the HTTP request, retrieve responses from the operator’s APIs.
The operator is required to receive and respond to HTTP requests sent by the game provider. Operators are
required to provide Token, AgentID and Key when calling this test tool for encryption and decryption
purpose.
.
URL /test/auth Method GET Return JSON
Description Send requests to operator’s auth API for testing

Request:

Parameter Type Require Description
AgentId string Yes Unique ID of the agent^
Key string Yes Validation Key (see in §1.1.2)^
Token string Yes Authorized key for requests (800 characters at most)
{
"Request Body": {
"reqId": "71d19bc8-90ec-4f25- 8472 - d6cb0361ab46",
"token": "793a4f6faf057353d44ee70cb6596cb5"
},
"Response": {
"errorCode": 0,
"message": "token verify success",
"username": "test_user_id",
"currency": "THB",
"balance": 101400,
"token": "793a4f6faf057353d44ee70cb6596cb5"
}
}

URL /test/bet Method GET Return JSON
Description Send requests to operator’s bet API for testing

Request:

Parameter Type Require Description
AgentId string Yes Unique ID of the agent^
Key string Yes Validation Key (see in §1.1.2)^
Token string Yes Authorized key for requests (800 characters at most)
IsFreeRound bool No True: offline payments
UserId string No
Player unique ID (by the operator’s special demands;
always appears in offline payments)
Default value from the testing tool will be used if not
provided.
{
"Request Body": {
"reqId": "dc996964-31ff- 4002 - a408-4800adc859ee",
"token": "52adb8d42ec8241dc3bd3e80d6227a87",
"currency": "THB",
"game": 9,
"round": 1699426561000030052,
"wagersTime": 1699426561,
"betAmount": 10,
"winloseAmount": 5
},
"Response": {
"errorCode": 0,
"message": "user bet success",
"username": "test_user_id",
"currency": "THB",
"balance": 101400,
"txId": 1699426561000030052,
"token": "52adb8d42ec8241dc3bd3e80d6227a87"
}
}

URL /test/cancelBet Method GET Return JSON
Description Send requests to operator’s cancelBet API for testing

Request:

Parameter Type Require Description
AgentId string Yes Unique ID of the agent^
Key string Yes Validation Key (see in §1.1.2)^
Token string Yes Authorized key for requests (800 characters at most)
IsFreeRound bool No True: offline payments
UserId string No
Player unique ID (by the operator’s special demands;
always appears in offline payments)
Default value from the testing tool will be used if not
provided.
{
"Request Body": {
"reqId": "dc996964-31ff- 4002 - a408-4800adc859ee",
"currency": "THB",
"game": 9,
"round": 1699426769000040045,
"betAmount": 10,
"winloseAmount": 5,
"userId": "test_userId",
"token": "52adb8d42ec8241dc3bd3e80d6227a87"
},
"[Bet Request Body]": {
"reqId": "b1efe8f5-3fed- 4445 - 8fee-f86d43e66e50",
"token": "52adb8d42ec8241dc3bd3e80d6227a87",
"currency": "THB",
"game": 9,
"round": 1699426769000040045,
"wagersTime": 1699426769,
"betAmount": 10,
"winloseAmount": 5
},
"Response": {
"errorCode": 0,
"message": "Cancel bet success",
"username": "test_user_id",
"currency": "THB",
"balance": 101400,
"txId": 1699426561000030052
}
}

URL <API URL>/test/sessionBet Method GET Return JSON
Description
Send bet and settle requests to operator’s sessionBet API for testing. If multiple bets are
applicable, two bet requests will be sent.

Request:

Parameter Type Require Description
AgentId string Yes Unique ID of the agent^
Key string Yes Validation Key (see in §1.1.2)^
Token string Yes Authorized key for requests (800 characters at most)
GameType int Yes
Game Types:
Bingo
Card games (without Preserve)
Card games (with Preserve)
UserId string No
Player unique ID (by the operator’s special demands;
always appears in offline payments)
Default value from the testing tool will be used if not
provided.
{
"Request Body (Bet 1)": {
"reqId": "efbe63b0-b2d0-457a-ab75-12dc63349084",
"token": "52adb8d42ec8241dc3bd3e80d6227a87",
"currency": "THB",
"game": 199,
"round": 1699428150000120079,
"wagersTime": 1699428150,
"betAmount": 100,
"winloseAmount": 0,
"sessionId": 1699428150000110079,
"type": 1,
"userId": "test_user_id",
"turnover": 0
},
"Response (Bet 1)": {
"errorCode": 0,
"message": "user bet success",
"username": "test_user_id",
"currency": "THB",
"balance": 101400,
"txId": 1699428150000120079,
"token": "52adb8d42ec8241dc3bd3e80d6227a87"
},
"Request Body (Settle)": {
"reqId": "b2da30b2-9c97- 4763 - 8923 - 2bc6e9ce7aa8",
"token": "52adb8d42ec8241dc3bd3e80d6227a87",
"currency": "THB",
"game": 199,
"round": 1699428408000170072,

"wagersTime": 1699428408,
"betAmount": 100,
"winloseAmount": 200,
"sessionId": 1699428150000110079,
"type": 2,
"userId": "test_user_id",
"turnover": 0
},
"Response (Settle)": {
"errorCode": 0,
"message": "user bet success",
"username": "test_user_id",
"currency": "THB",
"balance": 101500,
"txId": 1699428408000170072,
"token": "52adb8d42ec8241dc3bd3e80d6227a87"
}

}

URL /test/cancelSessionBet Method GET Return JSON
Description Send requests to operator’s cancelSessionBet API for testing

Request:

Parameter Type Require Description
AgentId string Yes Unique ID of the agent^
Key string Yes Validation Key (see in §1.1.2)^
Token string Yes Authorized key for requests (800 characters at most)
GameType int Yes
Game Types:
Bingo
Card games (without Preserve)
Card games (with Preserve)
UserId string No
Player unique ID (by the operator’s special demands;
always appears in offline payments)
Default value from the testing tool will be used if not
provided.
{
"Request Body": {
"reqId": "efbe63b0-b2d0-457a-ab75-12dc63349084",

"currency": "THB",
"game": 216,
"round": 1699428150000120079,
"betAmount": 100,
"winloseAmount": 0,
"userId": "test_user_id",
"token": "52adb8d42ec8241dc3bd3e80d6227a87",
"sessionId": 1699428150000110079,
"type": 1
},
"[Session Bet Request Body]": {
"reqId": "b2da30b2-9c97- 4763 - 8923 - 2bc6e9ce7aa8",
"token": "52adb8d42ec8241dc3bd3e80d6227a87",
"currency": "THB",
"game": 216,
"round": 1699428150000120079,
"wagersTime": 1699428408,
"betAmount": 100,
"winloseAmount": 0,
"sessionId": 1699428150000110079,
"type": 1,
"userId": "test_user_id",
"turnover": 0
},
"Response (Settle)": {
"errorCode": 0,
"message": "Cancel bet success",
"username": "test_user_id",
"currency": "THB",
"balance": 101500,
"txId": 1699428408000170072
}
}