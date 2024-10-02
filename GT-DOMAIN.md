# GT domain definition

- [Sports](#sports)
- [Categories](#categories)
- [Tournaments](#tournaments)
- [Events](#events)
- [Event statuses](#event-statuses)
- [Scores](#scores)
- [Markets](#markets)
- [Markets results](#markets-results)

## Sports
<details>
  <summary>Sport JSON description:</summary>

```json
{
    "Id": string, // sport string id
    "Name": {
        string: string //  key: value  where key is string language id (en, ro, fr, etc.), value - string
    },
    "Timestamp": DateTime ,// "2022-11-28T11:36:32.3409986Z", date time with time zone
    "DataVersion": int, // version of entity data
}
```
</details>

## Categories
Category is tournament group by country or championship type.

<details>
  <summary>Category JSON description:</summary>

```json
{
    "id": string, // Category string id
    "name": {
        string: string, //-  key: value map where left side is key is string language id (en, ro, fr, etc.), right side is value - string
    },
    "timestamp": DateTime, // date time with time zone
    "dataVersion": int, // version of category with current id, increments when one of category fields are changed
    "slug": string, // short name of category for SEO links
    "sport": string, // sport string id, "Football" for example
}
```
</details>

<details>
  <summary>Example:</summary>

```json
{
    "id": "d51986ee879f49e99e0597b820a34ff6",
    "name": {
        "en": "USA",
        "uk": "США",
        "uz": "AQSh",
        "vi": "Mỹ",
        "zn": "美国",
        "sw": "USA",
        "my": "USA",
        "ru": "США",
        "pt": "EUA",
        "ro": "SUA",
        "es": "Estados Unidos",
        "ms": "USA",
        "th": "สหรัฐอเมริกา",
        "fa": "ایالات متحده آمریکا",
        "zh": "美国"
    },
    "timestamp": "2022-12-22T20:10:28.7454716Z",
    "dataVersion": 75,
    "slug": "usa",
    "sport": "AmericanFootball"
}
```
</details>

## Tournaments
<details>
  <summary>Tournament JSON description:</summary>

```json
{
    "id": string, // Tournament string id 
    "categoryId": string , // parent ategory string id 
    "name": {
        string: string, //  key: value map where left side is key is string language id (en, ro, fr, etc.), right side is value - string 
    },
    "timestamp": DateTime // date time with time zone
    "dataVersion": int,  // version of category with current id, increments when one of category fields are changed
    "isInternational": bool, // shows if tournament is international or national championship
    "gender": string, // gender of competitors - man, women or none if it mixed 
    "competitorType": string, // type of competitors - players or teams or mixed (like cybersport for example)
    "slug": string, // short name of category for SEO links
    "sport": string, // sport string id, "Football" for example
}
```
</details>

<details>
  <summary>Example:</summary>

```json
{
    "id": "dacd14f5070b43b1b53d0382ff8567c7",
    "categoryId": "e1af5cbe212a4c25ace3413818cea243",
    "name": {
        "ru": "Женщины. WTT Star Contender. Гоа",
        "uk": "Жінки. WTT Star Contender. Гоа",
        "en": "Women. WTT Star Contender. Goa"
    },
    "timestamp": "2023-02-27T01:44:46.7622319Z",
    "dataVersion": 2,
    "isInternational": false,
    "gender": "Women",
    "competitorType": "Team",
    "slug": "women-wtt-star-contender-goa",
    "sport": "TableTennis",
}
```
</details>

## Events
<details>
  <summary>Event JSON description:</summary>

```json
{
    "id": string, // Event string id 
    "tournamentId":  string, // Tournament string id
    "tournamentName": {
        string: string, // name of tournament - "key: value" map where left side is key is string language id (en, ro, fr, etc.), right side is value - string
    },
    "categoryId": string, // Category string id
    "categoryName": {
        string: string, // name of category - "key: value" map where left side is key is string language id (en, ro, fr, etc.), right side is value - string
    },
    "name": {
        string: string, // name of event - "key: value" map where left side is key is string language id (en, ro, fr, etc.), right side is value - string
    },
    "tradingStatus": string, // shows trading status of event on GT Feed - open, supended 
    "stage": string, // shows current of event - prematch or Live
    "status": string,  // shows current of event - Created, Started, Paused, Finished, Retired, Abandoned, Interrupted, Cancelled, Postponed
    "type": string, // type of event - Match, Outrights, UniEvent - Event type "Unievent" relates to FreeForm functionality, which will be delivered on later stages upon readiness
    "startTime": DateTime, // date and time when event starting,
    "competitors": [
    {
      "id": string, // Event string id
      "name": {
        string: string, // name of competitor - "key: value" map where left side is key is string language id (en, ro, fr, etc.), right side is value - string
      },
      "slug":  string, // short name of category for SEO links
    }],
    "players": [
    {
      "id": string, // Event string id
      "name": {
        string: string, // name of competitor - "key: value" map where left side is key is string language id (en, ro, fr, etc.), right side is value - string
      },
      "slug":  string, // short name of category for SEO links
    }],
    "timestamp": DateTime // date time with time zone of last update
    "aggregateTimestamp": DateTime // date time with time zone of aggregation rntity data
    "dataVersion": int,  // version of event with if any operation from console are applied (Booking/Unbooking, Freeze/Unfreeze)
    "eventDataVersion": int,  // version of event with current id, increments when one of event fields are changed from Feed
    "plannedForPrematch": bool, // is planned this event for trading in prematch
    "plannedForLive": bool, // is planned this event for trading in live
    "sport": string, // string id of sport
    "sportName": {
        string: string, // name of sport - "key: value" map where left side is key is string language id (en, ro, fr, etc.), right side is value - string
    },
    "slug": string, // short name of category for SEO links
    "isCybersport": bool, // bool flag that shows if event is cyber sport
    "isActive": bool, // is active event - if it ready for trading now or in future
    "isOpenForTrading": bool // event is open for trading on GT Feed
    "isFrozen": bool // trading of event is suspended
    "sourceDataVersion": bool // original event version
    "modifiedBy": bool // show reason of update - feed, booking schema, or user name who initated changes from console
    "competitorType": string // type of event competitors -  None, Player, Pair, Team
    "outcomesCount": int // count of opened outcomes from active market events in feed (total)
    "liveBookingInfo": {} // information about booking in In-Play
    {        
        "isBooked": bool, //event is bookied
        "bookingType": int, //bookingType 1 - Auto by booking schema, 2 - manual booking
        "wasBooked": false, //event was booked before unbooking
        "autoBookingSchemaId": int //booking schema id
    },    
    "prematchBookingInfo": {} // information about booking in Prematch
     {       
        "isBooked": bool, //event is bookied
        "bookingType": int, //bookingType 1 - Auto by booking schema, 2 - manual booking
        "wasBooked": false, //event was booked before unbooking
        "autoBookingSchemaId": int //booking schema id
    },
}
```
</details>

<details>
  <summary>Example:</summary>

```json
{
    "id": "9688042",
    "tournamentId": "e911171d55394b159d98c4cd6daa06f2",
    "tournamentName": {
    "pt": "Mulheres. Trnava. Rígido. Qualificação",
    "sw": "Wanawake. Trnava. Hard. Zinazofuzu",
    "my": "Wanita. Trnava. Keras. Kelayakan",
    "ms": "Wanita. Trnava. Keras. Kelayakan",
    "uk": "Жінки. Трнава. Хард. Кваліфікація",
    "en": "Women. Trnava. Hard. Qualifying",
    "es": "Femenino. Trnava. Dura. Calificación",
    "ru": "Женщины. Трнава. Хард. Квалификация",
    "fa": "زنان. ترناوا. هارد. مقدماتی",
    "ro": "Feminin. Trnava. Hard. Calificări"
    },
    "categoryId": "a8988ff14804438bb67a5285824c0201",
    "categoryName": {
    "pt": "ITF",
    "uz": "ITF",
    "vi": "ITF",
    "fa": "فدراسیون بین المللی تنیس(آی تی اف)",
    "th": "ไอทีเอฟ",
    "en": "ITF",
    "ru": "ITF",
    "uk": "ITF",
    "my": "ITF",
    "ms": "ITF",
    "sw": "ITF",
    "ro": "ITF",
    "es": "ITF",
    "zh": "ITF",
    "zn": "ITF"
    },
    "name": {
    "pt": "Maria Bondarenko - Aneta Laboutkova",
    "fa": "Bondarenko Maria - Aneta Laboutkova",
    "sw": "Bondarenko Maria - Aneta Laboutkova",
    "ru": "Мария Бондаренко - Анета Лабуткова",
    "uk": "Марія Бондаренко - Анета Лабуткова",
    "en": "Maria Bondarenko - Aneta Laboutkova"
    },
    "tradingStatus": "Opened",
    "stage": "Live",
    "status": "Created",
    "type": "Match",
    "eventType": 0,
    "startTime": "2023-02-27T15:33:00Z",
    "competitors": [
    {
      "id": "169339",
      "name": {
        "pt": "Maria Bondarenko",
        "fa": "Bondarenko Maria",
        "sw": "Bondarenko Maria",
        "ru": "Мария Бондаренко",
        "uk": "Марія Бондаренко",
        "en": "Maria Bondarenko"
      },
      "nameMobile": {
        "ru": "Бондаренко М.",
        "en": "Bondarenko M."
      },
      "slug": "maria-bondarenko"
    },
    {
      "id": "67764",
      "name": {
        "pt": "Aneta Laboutkova",
        "fa": "Aneta Laboutkova",
        "sw": "Aneta Laboutkova",
        "ru": "Анета Лабуткова",
        "uk": "Анета Лабуткова",
        "en": "Aneta Laboutkova"
      },
      "nameMobile": {
        "ru": "Лабуткова А.",
        "uk": "Лабуткова А.",
        "en": "Laboutkova A."
      },
      "slug": "aneta-laboutkova"
    }
    ],
    "players": [],
    "timestamp": "2023-02-27T15:30:05.4282723Z",
    "aggregateTimestamp": "2023-02-27T15:30:05.557523Z",
    "removedTimestamp": null,
    "dataVersion": 21,
    "eventDataVersion": 21,
    "plannedForPrematch": true,
    "plannedForLive": true,
    "highlightId": null,
    "outcomesCount": 20,
    "betradarId": "39651139",
    "sport": "Tennis",
    "sportName": {
    "zh": "网球",
    "en": "Tennis",
    "sw": "Tenisi",
    "th": "เทนนิส ",
    "es": "Tenis",
    "fa": "تنیس",
    "zn": "网球",
    "vi": "Quần vợt",
    "my": "Tenis",
    "ru": "Теннис",
    "ms": "Tenis",
    "bn": "টেনিস",
    "pt": "Tênis",
    "ro": "Tenis",
    "bd": "টেনিস",
    "uz": "Tennis",
    "fr": "Tennis",
    "uk": "Теніс"
    },
    "slug": "maria-bondarenko-aneta-laboutkova",
    "isCybersport": false,
    "isActive": true,
    "isOpenForTrading": true,
    "isFrozen": false,
    "competitorType": "Player",
    "outcomesCount": 56
    "liveBookingInfo": {
        "isBooked": true,
        "bookingType": 1,
        "wasBooked": false,
        "autoBookingSchemaId": 1
    },
    "prematchBookingInfo": {
        "isBooked": true,
        "bookingType": 1,
        "wasBooked": false,
        "autoBookingSchemaId": 2
    }
}
```
</details>

## Event statuses
| Status      | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|-------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Created     | Business-case: event is created, is shown in event's list, available in trading line, trading started for Prematch<br>Markets for Prematch trading are available (Live-markets could become available few minutes prior to expected start-time)<br>Scoreboards are not available yet (match is not started yet, thus scores are absent).                                                                                                                                                                                                                |
| Started     | Business-case: event has started (start-time of event came), trading started for Live<br>Markets for Live trading are available, Prematch markets are not available any more<br>Scoreboards: receiving of scoreboards is started for Prematch and Live markets<br>Sometimes, as corner cases, scoreboards could be received prior to match start - depending on Sport (e.g. for market "Server" in Cricket)                                                                                                                                             |
| Paused      | Business-case: this status could be at scheduled break in the match (according to the event regulations) or short breaks based on referee decision<br>For some corner cases event's status still could be as Started<br>Markets for Live are available<br>Scoreboards: no scoreboards are updated by score changes, as match is paused. Updating of scores will continue to be provided after match resuming                                                                                                                                            |
| Finished    | Business-case: match is completed based on schedule (according to the event regulations)<br>In corner cases, by referee's decision - event's status may change (e.g. to Started)<br>Markets are not available any more<br>Scoreboards have been provided, as all event's markets resulted                                                                                                                                                                                                                                                               |
| Retired     | Business-case: refusal of one of the participants (team, player, couple) to continue the match. Competitor could refuse from match before event's start ("walkover")<br>Markets are not available any more<br>Scoreboards: are available only scoreboards, created before competitor's refusal from the event. Only they have been provided.<br>Thus, settlement is available: either based on already received scoreboards, or via Return (for markets, which were not resulted yet before competitor's refusal, and scoreboards will not be provided) | 
| Abandoned   | Business-case: "Coverage lost" for any reason (electricity, connection, etc)<br>Markets - are not available any more<br>Scoreboards - are available only scoreboards, created before coverage lost. Only they have been provided.<br>Thus, settlement is available: either based on already received scoreboards, or via Return (for markets, which were not resulted yet before competitor's refusal, and scoreboards will not be provided)                                                                                                            |                                                                                                            
| Interrupted | Business-case: break in the match due to external circumstances (e.g.: rain for Tennis). Supposedly event to be continued<br>Availability of markets is not guaranteed (depending on data-source)<br>Scoreboards: no scoreboards are provided, as match is interrupted. Scoreboards will continue to be provided after match resuming<br>If event was not resumed during predefined time (depends on each Sport, up to few days for Tennis) - all non-resulted markets could be settled as Return                                                       |                                                       
| Cancelled   | Business-case: match cancellation for all other reasons, mostly before event start-time (incl. technical reasons - odds/competitors are incorrectly provided)<br>Markets are not available<br>Scoreboards are not available, all settlements are done via Return                                                                                                                                                                                                                                                                                        |                                                                                                                                                                                                                                                                                     
| Postponed   | Business-case - event's start-time was rescheduled<br>Markets - are available for Prematch (Live-markets could become available few minutes prior to expected start-time)<br>Scoreboards are not available yet (match is not started yet, thus scores are absent)                                                                                                                                                                                                                                                                                       |

### Main lifecycle scenarios for Event:
Created → Started → Finished

Created → Started → Paused → Finished

Created → Started → Finished → Started → Finished

Created → Started → Retired

Created → Started → Interrupted→ Started → Finished

Created → Postponed → Started → Finished

Created → Started → Abandoned

Created → Cancelled

| TO →        | Created | Started | Paused | Finished | Retired | Abandoned | Interrupted | Cancelled | Postponed |
|-------------|---------|---------|--------|----------|---------|-----------|-------------|-----------|-----------| 
| FROM ↓      |         |         |        |          |         |           |             |           |           |
| Created     |         | ->      |        |          |         |           |             |   ->      |    ->     |
| Started     |         |         |  ->    |    ->    |   ->    |   ->      |   ->        |           |           |
| Paused      |         |         |        |    ->    |         |           |             |           |           |
| Finished    |         | ->      |        |          |         |           |             |           |           |
| Retired     |         |         |        |          |         |           |             |           |           |
| Abandoned   |         |         |        |          |         |           |             |           |           |
| Interrupted |         | ->      |        |          |         |           |             |           |           |
| Cancelled   |         |         |        |          |         |           |             |           |           |
| Postponed   |         | ->      |        |          |         |           |             |           |           |

## Scores
See full GT domain documentation pages for scores stages and periods per sport at https://api-docs.betgate.dev/score_description/index.html.

<details>
  <summary>Scoreboard JSON description:</summary>

```json
{
    "eventId": string, // Event string id 
    "timestamp": DateTime // date time with time zone of last update
    "dataVersion": int, //version of data entity
    "eventStatus": string,  // shows current of event - Created, Started, Paused, Finished, Retired, Abandoned, Interrupted, Cancelled, Postponed
    "currentGameStage": int, // stage,
    "currentGameSubStage": nullable int, // substage,
    "serverNumber": nullable int, // server number ,
    "timer": { //information about game timer
        "changeTime": DateTime, // date time with time zone of last timer change
        "currentTime": Date, // current date of timer
        "gameStageMaxTime": null,
        "isTimerOn": bool // shows if timer is on ,
        "timerDirection": string, // timer direction - Up or Down,
        "isGameStageTimer": bool // shows if timer actual only for current game stage
    },
    "server": "string, string, //Server - unknown or team1/team2 for teams sports
    "periodScores": [
    {
        "type": string, // description of period score type 
        "typePlatformId": int, // value of period score type Document with scoreboard description
        "period": int, // period of score 
        "subPeriod": nullable int, // subperiod of score ,
        "score": string, // score direction - "0-0" for example,
    }],
    "sport": string, // sport
}
```
</details>

<details>
  <summary>Example:</summary>

```json
{
    "eventId": "9689794",
    "timestamp": "2023-03-01T01:22:30.0476074Z",
    "dataVersion": 442,
    "eventStatus": "Started",
    "currentGameStage": 17,
    "currentGameSubStage": null,
    "serverNumber": null,
    "timer": {
        "changeTime": "2023-03-01T01:22:29.553Z",
        "currentTime": "00:26:14",
        "gameStageMaxTime": null,
        "isTimerOn": true,
        "timerDirection": "Up",
        "isGameStageTimer": false
    },
    "server": "Unknown",
    "periodScores": [
        {
            "type": "Points",
            "typePlatformId": 1010,
            "period": 1,
            "subPeriod": null,
            "score": "49-71"
        },
        {
            "type": "Points",
            "typePlatformId": 1010,
            "period": 2,
            "subPeriod": null,
            "score": "44-53"
        },
        {
            "type": "Points",
            "typePlatformId": 1010,
            "period": 3,
            "subPeriod": null,
            "score": "5-18"
        },
        {
            "type": "Points",
            "typePlatformId": 1010,
            "period": 8,
            "subPeriod": null,
            "score": "49-71"
        }
    ],
    "sport": "Basketball"
}
```
</details>

## Markets
The most important part regarding markets is that they always arrive as a snapshot of currently open or suspended markets. Thus, if a market from the previous snapshot is missing in later update, it means that market was closed and is not available for betting. **If markets message has empty markets or message body is empty, it means all event markets should be closed.**

See full GT domain documentation pages for market types, periods and result kinds per sport at https://api-docs.betgate.dev/markets_description/index.html.

### Market outcome selection key structure
```
[1,[2,3],[4,5],6,7,[8,9]]
```
* 1 - it's a marketType or marketId, which is described for every sport kind
* 2 and 3 - it's a market values
* 4 and 5 - is a market periods
* 6 - resultKind
* 7 - outcomeId
* 8 and 9 - outcome Parameters

<details>
  <summary>Market JSON description:</summary>

```json
{
    "eventId": string, // Event string id 
    "markets": [
    {
        "key": {
            "eventId": string, // Event string id 
            "tradingType": int, // Type of trading 
            "marketType": int, // Type of market, for detail information please look at document described markets or on metadata service 
            "period": int, // Period of match 
            "subPeriod": nullable int // Subperiod for match - depends on sport
        },
        "marketItems": [  //markey item is trading position like as Total, Fora, etc.
        {
            "values": [array of string], //market item values
            "isOpen": bool, //shows that market is open for trading
            "lineItemId": string, //parent market group for current market, required for bet acceptance, if it empty please look at market lineItemId
            "outcomes": [ //array of outcomes
            {
                "outcomeType": int, //id type of outcome
                "outcomeValues": [array of string], //parameters of outcome
                "price": double, //price or coefficient for outcome
                "status": string, //status of outcome - open, suspended or removed
                "lineItemId": string, //parent market group for current market, required for bet acceptance, if it empty please look at market item lineItemId
                "selectionKey": string, //outcome identificator for bet acceptance
                "dataVersion": int //version of data entity
            }
          ],
          "oddsMultipliers": Map, //map with brand as a key, values are odds multipliers that should be multiply to coefficient per brand
          "isRemoved": bool // shows if market item was removed in current update
          "tradingInfoCustomization": Map // map with brand as a key, values are customization of limits and delay per brand
        }
      ],
      "status": string, // market status - open, suspended or removed
      "stage": string,  //market stage - Live or Prematch
      "parlaySize": int, //parlay size
      "lineItemId": string, //parent market group for current market, required for bet acceptance, if it empty please look at market item lineItemId
      "dataVersion": int, //version of data entity
      "sport": string, // market sport
      "visibility": Map, //map with visibility of market per brand
      "tradingInfo": { //trading information 
        "limit": {
            "type": string, // type of limit on bet - Liability or Bet
            "amount": int // amount of limit in US $
        },
        "delay": double // delay for bet acceptance in seconds
      }
    }],
    "dataVersion": int, //version of data entity
    "timestamp": DateTime // date time with time zone of last update
    "isFrozen": bool, //shows that markets are suspended for trading
    "tradingInfos": [  //trading information for matkets group (line item)
    {
        "lineItemId": string //id of line item for which apply this trading information ,
        "limit": {
            "type": "Liability",    // tpe of limit, supported Liability only
            "amount": int // amount of limit
        },
        "delay": int, // delay for bet acception
        "parlaySize": int, // allowed express size
        "isCashoutAllowed": bool, // cashout allowed or not
        "isOveraskAllowed": bool, //overask allowed or not
    }],
    "isBookedForLive": bool, //show that markets was booked for In-Play stage
    "isBookedForPrematch": bool //show that markets was booked for Prematch stage
}
```
</details>

<details>
  <summary>Example:</summary>

```json
{
  "eventId": "10579790",
  "stage": "Live",
  "markets": [
    {
      "sourceDataVersion": 19,
      "visibility": {
        "default": true,
        "cM1": true,
        "cM3": true
      },
      "key": {
        "eventId": "10579790",
        "tradingType": 1,
        "marketType": 10,
        "period": 0,
        "subPeriod": null,
        "layout": null
      },
      "marketItems": [
        {
          "values": [],
          "isOpen": true,
          "outcomes": [
            {
              "outcomeType": 16,
              "outcomeValues": [],
              "price": 1.87,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[10,[],[0],1,16,[]]",
              "dataVersion": 10,
              "probability": null,
              "limitPercentage": 1
            },
            {
              "outcomeType": 17,
              "outcomeValues": [],
              "price": 4.4,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[10,[],[0],1,17,[]]",
              "dataVersion": 12,
              "probability": null,
              "limitPercentage": 1
            },
            {
              "outcomeType": 18,
              "outcomeValues": [],
              "price": 8,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[10,[],[0],1,18,[]]",
              "dataVersion": 10,
              "probability": null,
              "limitPercentage": 1
            },
            {
              "outcomeType": 19,
              "outcomeValues": [],
              "price": 19,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[10,[],[0],1,19,[]]",
              "dataVersion": 6,
              "probability": null,
              "limitPercentage": 1
            },
            {
              "outcomeType": 20,
              "outcomeValues": [],
              "price": 9.5,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[10,[],[0],1,20,[]]",
              "dataVersion": 7,
              "probability": null,
              "limitPercentage": 1
            },
            {
              "outcomeType": 21,
              "outcomeValues": [],
              "price": 9,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[10,[],[0],1,21,[]]",
              "dataVersion": 8,
              "probability": null,
              "limitPercentage": 1
            },
            {
              "outcomeType": 22,
              "outcomeValues": [],
              "price": 51,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[10,[],[0],1,22,[]]",
              "dataVersion": 3,
              "probability": null,
              "limitPercentage": 1
            },
            {
              "outcomeType": 23,
              "outcomeValues": [],
              "price": 45,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[10,[],[0],1,23,[]]",
              "dataVersion": 5,
              "probability": null,
              "limitPercentage": 1
            },
            {
              "outcomeType": 24,
              "outcomeValues": [],
              "price": 20,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[10,[],[0],1,24,[]]",
              "dataVersion": 8,
              "probability": null,
              "limitPercentage": 1
            }
          ],
          "oddsMultipliers": {
            "default": 1,
            "cM1": 1.0481,
            "cM2": 1.0480
          },
          "tradingInfoCustomization": {
            "default": {
              "absoluteLimit": null,
              "delay": null
            },
            "cM1": {
              "absoluteLimit": null,
              "delay": null
            },
            "cM3": {
              "absoluteLimit": null,
              "delay": null
            }
          },
          "isRemoved": false
        }
      ],
      "status": "Opened",
      "stage": "Live",
      "parlaySize": 0,
      "dataVersion": 1,
      "sport": "Football",
      "tradingInfo": {
        "trader": "Beter_UF",
        "limit": {
          "type": "Liability",
          "amount": 300
        },
        "delay": 6
      },
      "isFrozen": false,
      "sourceTimestamp": "2023-10-31T14:21:04.104+00:00"
    },
    {
      "sourceDataVersion": 19,
      "visibility": {
        "default": true,
        "cM1": true,
        "cM3": true
      },
      "key": {
        "eventId": "10579790",
        "tradingType": 1,
        "marketType": 118,
        "period": 0,
        "subPeriod": null,
        "layout": null
      },
      "marketItems": [
        {
          "values": [
            "2"
          ],
          "isOpen": true,
          "outcomes": [
            {
              "outcomeType": 11,
              "outcomeValues": [],
              "price": 3.5,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[118,[2],[0],1,11,[]]",
              "dataVersion": 6,
              "probability": null,
              "limitPercentage": 1
            },
            {
              "outcomeType": 12,
              "outcomeValues": [],
              "price": 4.2,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[118,[2],[0],1,12,[]]",
              "dataVersion": 12,
              "probability": null,
              "limitPercentage": 1
            },
            {
              "outcomeType": 13,
              "outcomeValues": [],
              "price": 1.7,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[118,[2],[0],1,13,[]]",
              "dataVersion": 11,
              "probability": null,
              "limitPercentage": 1
            }
          ],
          "oddsMultipliers": {
            "default": 1,
            "cM1": 1.0481,
            "cM2": 1.0480
          },
          "tradingInfoCustomization": {
            "default": {
              "absoluteLimit": null,
              "delay": null
            },
            "cM1": {
              "absoluteLimit": null,
              "delay": null
            },
            "cM3": {
              "absoluteLimit": null,
              "delay": null
            }
          },
          "isRemoved": false
        }
      ],
      "status": "Opened",
      "stage": "Live",
      "parlaySize": 0,
      "dataVersion": 1,
      "sport": "Football",
      "tradingInfo": {
        "trader": "Beter_UF",
        "limit": {
          "type": "Liability",
          "amount": 300
        },
        "delay": 6
      },
      "isFrozen": false,
      "sourceTimestamp": "2023-10-31T14:21:04.104+00:00"
    },
    {
      "sourceDataVersion": 19,
      "visibility": {
        "default": true,
        "cM1": true,
        "cM3": true
      },
      "key": {
        "eventId": "10579790",
        "tradingType": 1,
        "marketType": 16,
        "period": 0,
        "subPeriod": null,
        "layout": null
      },
      "marketItems": [
        {
          "values": [],
          "isOpen": true,
          "outcomes": [
            {
              "outcomeType": 102,
              "outcomeValues": [
                "1",
                "0"
              ],
              "price": 4.2,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[16,[],[0],1,102,[1,0]]",
              "dataVersion": 12,
              "probability": null,
              "limitPercentage": 1
            },
            {
              "outcomeType": 102,
              "outcomeValues": [
                "1",
                "1"
              ],
              "price": 5.25,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[16,[],[0],1,102,[1,1]]",
              "dataVersion": 9,
              "probability": null,
              "limitPercentage": 1
            },
            {
              "outcomeType": 102,
              "outcomeValues": [
                "1",
                "3"
              ],
              "price": 19,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[16,[],[0],1,102,[1,3]]",
              "dataVersion": 6,
              "probability": null,
              "limitPercentage": 1
            },
            {
              "outcomeType": 102,
              "outcomeValues": [
                "1",
                "4"
              ],
              "price": 41,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[16,[],[0],1,102,[1,4]]",
              "dataVersion": 5,
              "probability": null,
              "limitPercentage": 1
            },
            {
              "outcomeType": 102,
              "outcomeValues": [
                "2",
                "1"
              ],
              "price": 9.2,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[16,[],[0],1,102,[2,1]]",
              "dataVersion": 6,
              "probability": null,
              "limitPercentage": 1
            },
            {
              "outcomeType": 102,
              "outcomeValues": [
                "2",
                "2"
              ],
              "price": 16,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[16,[],[0],1,102,[2,2]]",
              "dataVersion": 5,
              "probability": null,
              "limitPercentage": 1
            },
            {
              "outcomeType": 102,
              "outcomeValues": [
                "2",
                "3"
              ],
              "price": 30,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[16,[],[0],1,102,[2,3]]",
              "dataVersion": 8,
              "probability": null,
              "limitPercentage": 1
            },
            {
              "outcomeType": 102,
              "outcomeValues": [
                "2",
                "4"
              ],
              "price": 51,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[16,[],[0],1,102,[2,4]]",
              "dataVersion": 5,
              "probability": null,
              "limitPercentage": 1
            },
            {
              "outcomeType": 102,
              "outcomeValues": [
                "2",
                "5"
              ],
              "price": 67,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[16,[],[0],1,102,[2,5]]",
              "dataVersion": 4,
              "probability": null,
              "limitPercentage": 1
            },
            {
              "outcomeType": 102,
              "outcomeValues": [
                "3",
                "1"
              ],
              "price": 27,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[16,[],[0],1,102,[3,1]]",
              "dataVersion": 5,
              "probability": null,
              "limitPercentage": 1
            },
            {
              "outcomeType": 102,
              "outcomeValues": [
                "3",
                "2"
              ],
              "price": 37,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[16,[],[0],1,102,[3,2]]",
              "dataVersion": 6,
              "probability": null,
              "limitPercentage": 1
            },
            {
              "outcomeType": 102,
              "outcomeValues": [
                "3",
                "3"
              ],
              "price": 55,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[16,[],[0],1,102,[3,3]]",
              "dataVersion": 7,
              "probability": null,
              "limitPercentage": 1
            },
            {
              "outcomeType": 102,
              "outcomeValues": [
                "3",
                "4"
              ],
              "price": 67,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[16,[],[0],1,102,[3,4]]",
              "dataVersion": 4,
              "probability": null,
              "limitPercentage": 1
            },
            {
              "outcomeType": 102,
              "outcomeValues": [
                "1",
                "2"
              ],
              "price": 8.5,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[16,[],[0],1,102,[1,2]]",
              "dataVersion": 5,
              "probability": null,
              "limitPercentage": 1
            },
            {
              "outcomeType": 102,
              "outcomeValues": [
                "1",
                "5"
              ],
              "price": 61,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[16,[],[0],1,102,[1,5]]",
              "dataVersion": 4,
              "probability": null,
              "limitPercentage": 1
            },
            {
              "outcomeType": 102,
              "outcomeValues": [
                "1",
                "6"
              ],
              "price": 67,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[16,[],[0],1,102,[1,6]]",
              "dataVersion": 2,
              "probability": null,
              "limitPercentage": 1
            },
            {
              "outcomeType": 102,
              "outcomeValues": [
                "2",
                "0"
              ],
              "price": 10,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[16,[],[0],1,102,[2,0]]",
              "dataVersion": 6,
              "probability": null,
              "limitPercentage": 1
            },
            {
              "outcomeType": 102,
              "outcomeValues": [
                "3",
                "0"
              ],
              "price": 27,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[16,[],[0],1,102,[3,0]]",
              "dataVersion": 3,
              "probability": null,
              "limitPercentage": 1
            },
            {
              "outcomeType": 102,
              "outcomeValues": [
                "3",
                "5"
              ],
              "price": 67,
              "status": "Suspended",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[16,[],[0],1,102,[3,5]]",
              "dataVersion": 3,
              "probability": null,
              "limitPercentage": 1
            },
            {
              "outcomeType": 102,
              "outcomeValues": [
                "4",
                "0"
              ],
              "price": 55,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[16,[],[0],1,102,[4,0]]",
              "dataVersion": 3,
              "probability": null,
              "limitPercentage": 1
            },
            {
              "outcomeType": 102,
              "outcomeValues": [
                "4",
                "1"
              ],
              "price": 55,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[16,[],[0],1,102,[4,1]]",
              "dataVersion": 4,
              "probability": null,
              "limitPercentage": 1
            },
            {
              "outcomeType": 102,
              "outcomeValues": [
                "4",
                "2"
              ],
              "price": 61,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[16,[],[0],1,102,[4,2]]",
              "dataVersion": 4,
              "probability": null,
              "limitPercentage": 1
            },
            {
              "outcomeType": 102,
              "outcomeValues": [
                "4",
                "3"
              ],
              "price": 67,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[16,[],[0],1,102,[4,3]]",
              "dataVersion": 3,
              "probability": null,
              "limitPercentage": 1
            },
            {
              "outcomeType": 102,
              "outcomeValues": [
                "5",
                "0"
              ],
              "price": 67,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[16,[],[0],1,102,[5,0]]",
              "dataVersion": 2,
              "probability": null,
              "limitPercentage": 1
            },
            {
              "outcomeType": 102,
              "outcomeValues": [
                "5",
                "1"
              ],
              "price": 67,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[16,[],[0],1,102,[5,1]]",
              "dataVersion": 4,
              "probability": null,
              "limitPercentage": 1
            }
          ],
          "oddsMultipliers": {
            "default": 1,
            "cM1": 1.0481,
            "cM2": 1.0480
          },
          "tradingInfoCustomization": {
            "default": {
              "absoluteLimit": null,
              "delay": null
            },
            "cM1": {
              "absoluteLimit": null,
              "delay": null
            },
            "cM3": {
              "absoluteLimit": null,
              "delay": null
            }
          },
          "isRemoved": false
        }
      ],
      "status": "Opened",
      "stage": "Live",
      "parlaySize": 0,
      "dataVersion": 1,
      "sport": "Football",
      "tradingInfo": {
        "trader": "Beter_UF",
        "limit": {
          "type": "Liability",
          "amount": 300
        },
        "delay": 6
      },
      "isFrozen": false,
      "sourceTimestamp": "2023-10-31T14:21:04.104+00:00"
    },
    {
      "sourceDataVersion": 19,
      "visibility": {
        "default": true,
        "cM1": true,
        "cM3": true
      },
      "key": {
        "eventId": "10579790",
        "tradingType": 1,
        "marketType": 195,
        "period": 0,
        "subPeriod": null,
        "layout": null
      },
      "marketItems": [
        {
          "values": [
            "2.25"
          ],
          "isOpen": true,
          "outcomes": [
            {
              "outcomeType": 4,
              "outcomeValues": [],
              "price": 1.65,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[195,[2.25],[0],1,4,[]]",
              "dataVersion": 4,
              "probability": null,
              "limitPercentage": 1
            },
            {
              "outcomeType": 5,
              "outcomeValues": [],
              "price": 2.1,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[195,[2.25],[0],1,5,[]]",
              "dataVersion": 4,
              "probability": null,
              "limitPercentage": 1
            }
          ],
          "oddsMultipliers": {
            "default": 1,
            "cM1": 1.0481,
            "cM2": 1.0480
          },
          "tradingInfoCustomization": {
            "default": {
              "absoluteLimit": null,
              "delay": null
            },
            "cM1": {
              "absoluteLimit": null,
              "delay": null
            },
            "cM3": {
              "absoluteLimit": null,
              "delay": null
            }
          },
          "isRemoved": false
        },
        {
          "values": [
            "2.75"
          ],
          "isOpen": true,
          "outcomes": [
            {
              "outcomeType": 4,
              "outcomeValues": [],
              "price": 2.3,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[195,[2.75],[0],1,4,[]]",
              "dataVersion": 10,
              "probability": null,
              "limitPercentage": 1
            },
            {
              "outcomeType": 5,
              "outcomeValues": [],
              "price": 1.55,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[195,[2.75],[0],1,5,[]]",
              "dataVersion": 10,
              "probability": null,
              "limitPercentage": 1
            }
          ],
          "oddsMultipliers": {
            "default": 1,
            "cM1": 1.0481,
            "cM2": 1.0480
          },
          "tradingInfoCustomization": {
            "default": {
              "absoluteLimit": null,
              "delay": null
            },
            "cM1": {
              "absoluteLimit": null,
              "delay": null
            },
            "cM3": {
              "absoluteLimit": null,
              "delay": null
            }
          },
          "isRemoved": false
        }
      ],
      "status": "Opened",
      "stage": "Live",
      "parlaySize": 0,
      "dataVersion": 1,
      "sport": "Football",
      "tradingInfo": {
        "trader": "Beter_UF",
        "limit": {
          "type": "Liability",
          "amount": 300
        },
        "delay": 6
      },
      "isFrozen": false,
      "sourceTimestamp": "2023-10-31T14:21:04.104+00:00"
    },
    {
      "sourceDataVersion": 19,
      "visibility": {
        "default": true,
        "cM1": true,
        "cM3": true
      },
      "key": {
        "eventId": "10579790",
        "tradingType": 1,
        "marketType": 2,
        "period": 0,
        "subPeriod": null,
        "layout": null
      },
      "marketItems": [
        {
          "values": [],
          "isOpen": true,
          "outcomes": [
            {
              "outcomeType": 0,
              "outcomeValues": [],
              "price": 1.8,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[2,[],[0],1,0,[]]",
              "dataVersion": 13,
              "probability": null,
              "limitPercentage": 1
            },
            {
              "outcomeType": 1,
              "outcomeValues": [],
              "price": 3.25,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[2,[],[0],1,1,[]]",
              "dataVersion": 14,
              "probability": null,
              "limitPercentage": 1
            },
            {
              "outcomeType": 3,
              "outcomeValues": [],
              "price": 4.05,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[2,[],[0],1,3,[]]",
              "dataVersion": 15,
              "probability": null,
              "limitPercentage": 1
            }
          ],
          "oddsMultipliers": {
            "default": 1.0046,
            "cM1": 0.444,
            "cM3": 1.0046
          },
          "tradingInfoCustomization": {
            "default": {
              "absoluteLimit": null,
              "delay": null
            },
            "cM1": {
              "absoluteLimit": 12,
              "delay": 12
            },
            "cM3": {
              "absoluteLimit": null,
              "delay": null
            }
          },
          "isRemoved": false
        }
      ],
      "status": "Opened",
      "stage": "Live",
      "parlaySize": 0,
      "dataVersion": 1,
      "sport": "Football",
      "tradingInfo": {
        "trader": "Beter_UF",
        "limit": {
          "type": "Liability",
          "amount": 300
        },
        "delay": 6
      },
      "isFrozen": false,
      "sourceTimestamp": "2023-10-31T14:21:04.104+00:00"
    },
    {
      "sourceDataVersion": 19,
      "visibility": {
        "default": true,
        "cM1": true,
        "cM3": true
      },
      "key": {
        "eventId": "10579790",
        "tradingType": 1,
        "marketType": 2,
        "period": 1,
        "subPeriod": null,
        "layout": null
      },
      "marketItems": [
        {
          "values": [],
          "isOpen": true,
          "outcomes": [
            {
              "outcomeType": 0,
              "outcomeValues": [],
              "price": 1.2,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[2,[],[1],1,0,[]]",
              "dataVersion": 17,
              "probability": null,
              "limitPercentage": 1
            },
            {
              "outcomeType": 1,
              "outcomeValues": [],
              "price": 4.4,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[2,[],[1],1,1,[]]",
              "dataVersion": 17,
              "probability": null,
              "limitPercentage": 1
            },
            {
              "outcomeType": 3,
              "outcomeValues": [],
              "price": 18,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[2,[],[1],1,3,[]]",
              "dataVersion": 15,
              "probability": null,
              "limitPercentage": 1
            }
          ],
          "oddsMultipliers": {
            "default": 1,
            "cM1": 1.0481,
            "cM2": 1.0480
          },
          "tradingInfoCustomization": {
            "default": {
              "absoluteLimit": null,
              "delay": null
            },
            "cM1": {
              "absoluteLimit": null,
              "delay": null
            },
            "cM3": {
              "absoluteLimit": null,
              "delay": null
            }
          },
          "isRemoved": false
        }
      ],
      "status": "Opened",
      "stage": "Live",
      "parlaySize": 0,
      "dataVersion": 1,
      "sport": "Football",
      "tradingInfo": {
        "trader": "Beter_UF",
        "limit": {
          "type": "Liability",
          "amount": 300
        },
        "delay": 6
      },
      "isFrozen": false,
      "sourceTimestamp": "2023-10-31T14:21:04.104+00:00"
    },
    {
      "sourceDataVersion": 19,
      "visibility": {
        "default": true,
        "cM1": true,
        "cM3": true
      },
      "key": {
        "eventId": "10579790",
        "tradingType": 1,
        "marketType": 28,
        "period": 0,
        "subPeriod": null,
        "layout": null
      },
      "marketItems": [
        {
          "values": [],
          "isOpen": true,
          "outcomes": [
            {
              "outcomeType": 14,
              "outcomeValues": [],
              "price": 1.42,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[28,[],[0],1,14,[]]",
              "dataVersion": 7,
              "probability": null,
              "limitPercentage": 1
            },
            {
              "outcomeType": 15,
              "outcomeValues": [],
              "price": 2.65,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[28,[],[0],1,15,[]]",
              "dataVersion": 7,
              "probability": null,
              "limitPercentage": 1
            }
          ],
          "oddsMultipliers": {
            "default": 1,
            "cM1": 1.0481,
            "cM2": 1.0480
          },
          "tradingInfoCustomization": {
            "default": {
              "absoluteLimit": null,
              "delay": null
            },
            "cM1": {
              "absoluteLimit": null,
              "delay": null
            },
            "cM3": {
              "absoluteLimit": null,
              "delay": null
            }
          },
          "isRemoved": false
        }
      ],
      "status": "Opened",
      "stage": "Live",
      "parlaySize": 0,
      "dataVersion": 1,
      "sport": "Football",
      "tradingInfo": {
        "trader": "Beter_UF",
        "limit": {
          "type": "Liability",
          "amount": 300
        },
        "delay": 6
      },
      "isFrozen": false,
      "sourceTimestamp": "2023-10-31T14:21:04.104+00:00"
    },
    {
      "sourceDataVersion": 19,
      "visibility": {
        "default": true,
        "cM1": true,
        "cM3": true
      },
      "key": {
        "eventId": "10579790",
        "tradingType": 1,
        "marketType": 3,
        "period": 0,
        "subPeriod": null,
        "layout": null
      },
      "marketItems": [
        {
          "values": [],
          "isOpen": true,
          "outcomes": [
            {
              "outcomeType": 8,
              "outcomeValues": [],
              "price": 1.2,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[3,[],[0],1,8,[]]",
              "dataVersion": 7,
              "probability": null,
              "limitPercentage": 1
            },
            {
              "outcomeType": 9,
              "outcomeValues": [],
              "price": 1.9,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[3,[],[0],1,9,[]]",
              "dataVersion": 8,
              "probability": null,
              "limitPercentage": 1
            },
            {
              "outcomeType": 10,
              "outcomeValues": [],
              "price": 1.3,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[3,[],[0],1,10,[]]",
              "dataVersion": 6,
              "probability": null,
              "limitPercentage": 1
            }
          ],
          "oddsMultipliers": {
            "default": 0.9792,
            "cM1": 0.4257,
            "cM3": 0.9792
          },
          "tradingInfoCustomization": {
            "default": {
              "absoluteLimit": null,
              "delay": null
            },
            "cM1": {
              "absoluteLimit": 12,
              "delay": 12
            },
            "cM3": {
              "absoluteLimit": null,
              "delay": null
            }
          },
          "isRemoved": false
        }
      ],
      "status": "Opened",
      "stage": "Live",
      "parlaySize": 0,
      "dataVersion": 1,
      "sport": "Football",
      "tradingInfo": {
        "trader": "Beter_UF",
        "limit": {
          "type": "Liability",
          "amount": 300
        },
        "delay": 6
      },
      "isFrozen": false,
      "sourceTimestamp": "2023-10-31T14:21:04.104+00:00"
    },
    {
      "sourceDataVersion": 19,
      "visibility": {
        "default": true,
        "cM1": true,
        "cM3": true
      },
      "key": {
        "eventId": "10579790",
        "tradingType": 1,
        "marketType": 3,
        "period": 1,
        "subPeriod": null,
        "layout": null
      },
      "marketItems": [
        {
          "values": [],
          "isOpen": true,
          "outcomes": [
            {
              "outcomeType": 8,
              "outcomeValues": [],
              "price": 1.01,
              "status": "Suspended",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[3,[],[1],1,8,[]]",
              "dataVersion": 4,
              "probability": null,
              "limitPercentage": 1
            },
            {
              "outcomeType": 9,
              "outcomeValues": [],
              "price": 4,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[3,[],[1],1,9,[]]",
              "dataVersion": 11,
              "probability": null,
              "limitPercentage": 1
            },
            {
              "outcomeType": 10,
              "outcomeValues": [],
              "price": 1.17,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[3,[],[1],1,10,[]]",
              "dataVersion": 10,
              "probability": null,
              "limitPercentage": 1
            }
          ],
          "oddsMultipliers": {
            "default": 1,
            "cM1": 1.0481,
            "cM2": 1.0480
          },
          "tradingInfoCustomization": {
            "default": {
              "absoluteLimit": null,
              "delay": null
            },
            "cM1": {
              "absoluteLimit": null,
              "delay": null
            },
            "cM3": {
              "absoluteLimit": null,
              "delay": null
            }
          },
          "isRemoved": false
        }
      ],
      "status": "Opened",
      "stage": "Live",
      "parlaySize": 0,
      "dataVersion": 1,
      "sport": "Football",
      "tradingInfo": {
        "trader": "Beter_UF",
        "limit": {
          "type": "Liability",
          "amount": 300
        },
        "delay": 6
      },
      "isFrozen": false,
      "sourceTimestamp": "2023-10-31T14:21:04.104+00:00"
    },
    {
      "sourceDataVersion": 19,
      "visibility": {
        "default": true,
        "cM1": true,
        "cM3": true
      },
      "key": {
        "eventId": "10579790",
        "tradingType": 1,
        "marketType": 4,
        "period": 0,
        "subPeriod": null,
        "layout": null
      },
      "marketItems": [
        {
          "values": [
            "-1"
          ],
          "isOpen": true,
          "outcomes": [
            {
              "outcomeType": 86,
              "outcomeValues": [],
              "price": 3.5,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[4,[-1],[0],1,86,[]]",
              "dataVersion": 4,
              "probability": null,
              "limitPercentage": 0.25
            },
            {
              "outcomeType": 87,
              "outcomeValues": [],
              "price": 1.26,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[4,[-1],[0],1,87,[]]",
              "dataVersion": 4,
              "probability": null,
              "limitPercentage": 0.25
            }
          ],
          "oddsMultipliers": {
            "default": 0.9984,
            "cM1": 0.4317,
            "cM3": 0.9984
          },
          "tradingInfoCustomization": {
            "default": {
              "absoluteLimit": null,
              "delay": null
            },
            "cM1": {
              "absoluteLimit": 12,
              "delay": 12
            },
            "cM3": {
              "absoluteLimit": null,
              "delay": null
            }
          },
          "isRemoved": false
        },
        {
          "values": [
            "0"
          ],
          "isOpen": true,
          "outcomes": [
            {
              "outcomeType": 86,
              "outcomeValues": [],
              "price": 1.33,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[4,[0],[0],1,86,[]]",
              "dataVersion": 9,
              "probability": null,
              "limitPercentage": 0.25
            },
            {
              "outcomeType": 87,
              "outcomeValues": [],
              "price": 3.05,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[4,[0],[0],1,87,[]]",
              "dataVersion": 9,
              "probability": null,
              "limitPercentage": 0.25
            }
          ],
          "oddsMultipliers": {
            "default": 0.9987,
            "cM1": 0.4318,
            "cM3": 0.9987
          },
          "tradingInfoCustomization": {
            "default": {
              "absoluteLimit": null,
              "delay": null
            },
            "cM1": {
              "absoluteLimit": 12,
              "delay": 12
            },
            "cM3": {
              "absoluteLimit": null,
              "delay": null
            }
          },
          "isRemoved": false
        }
      ],
      "status": "Opened",
      "stage": "Live",
      "parlaySize": 0,
      "dataVersion": 1,
      "sport": "Football",
      "tradingInfo": {
        "trader": "Beter_UF",
        "limit": {
          "type": "Liability",
          "amount": 300
        },
        "delay": 6
      },
      "isFrozen": false,
      "sourceTimestamp": "2023-10-31T14:21:04.104+00:00"
    },
    {
      "sourceDataVersion": 19,
      "visibility": {
        "default": true,
        "cM1": true,
        "cM3": true
      },
      "key": {
        "eventId": "10579790",
        "tradingType": 1,
        "marketType": 401,
        "period": 0,
        "subPeriod": null,
        "layout": null
      },
      "marketItems": [
        {
          "values": [],
          "isOpen": true,
          "outcomes": [
            {
              "outcomeType": 95,
              "outcomeValues": [],
              "price": 6,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[401,[],[0],1,95,[]]",
              "dataVersion": 12,
              "probability": null,
              "limitPercentage": 1
            },
            {
              "outcomeType": 96,
              "outcomeValues": [],
              "price": 2.65,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[401,[],[0],1,96,[]]",
              "dataVersion": 7,
              "probability": null,
              "limitPercentage": 1
            },
            {
              "outcomeType": 97,
              "outcomeValues": [],
              "price": 3.25,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[401,[],[0],1,97,[]]",
              "dataVersion": 8,
              "probability": null,
              "limitPercentage": 1
            },
            {
              "outcomeType": 106,
              "outcomeValues": [],
              "price": 4.05,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[401,[],[0],1,106,[]]",
              "dataVersion": 9,
              "probability": null,
              "limitPercentage": 1
            }
          ],
          "oddsMultipliers": {
            "default": 1,
            "cM1": 1.0481,
            "cM2": 1.0480
          },
          "tradingInfoCustomization": {
            "default": {
              "absoluteLimit": null,
              "delay": null
            },
            "cM1": {
              "absoluteLimit": null,
              "delay": null
            },
            "cM3": {
              "absoluteLimit": null,
              "delay": null
            }
          },
          "isRemoved": false
        }
      ],
      "status": "Opened",
      "stage": "Live",
      "parlaySize": 0,
      "dataVersion": 1,
      "sport": "Football",
      "tradingInfo": {
        "trader": "Beter_UF",
        "limit": {
          "type": "Liability",
          "amount": 300
        },
        "delay": 6
      },
      "isFrozen": false,
      "sourceTimestamp": "2023-10-31T14:21:04.104+00:00"
    },
    {
      "sourceDataVersion": 19,
      "visibility": {
        "default": true,
        "cM1": true,
        "cM3": true
      },
      "key": {
        "eventId": "10579790",
        "tradingType": 1,
        "marketType": 5,
        "period": 1,
        "subPeriod": null,
        "layout": null
      },
      "marketItems": [
        {
          "values": [
            "1.5"
          ],
          "isOpen": true,
          "outcomes": [
            {
              "outcomeType": 4,
              "outcomeValues": [],
              "price": 2.5,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[5,[1.5],[1],1,4,[]]",
              "dataVersion": 8,
              "probability": null,
              "limitPercentage": 1
            },
            {
              "outcomeType": 5,
              "outcomeValues": [],
              "price": 1.47,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[5,[1.5],[1],1,5,[]]",
              "dataVersion": 8,
              "probability": null,
              "limitPercentage": 1
            }
          ],
          "oddsMultipliers": {
            "default": 1,
            "cM1": 1.0481,
            "cM2": 1.0480
          },
          "tradingInfoCustomization": {
            "default": {
              "absoluteLimit": null,
              "delay": null
            },
            "cM1": {
              "absoluteLimit": null,
              "delay": null
            },
            "cM3": {
              "absoluteLimit": null,
              "delay": null
            }
          },
          "isRemoved": false
        }
      ],
      "status": "Opened",
      "stage": "Live",
      "parlaySize": 0,
      "dataVersion": 1,
      "sport": "Football",
      "tradingInfo": {
        "trader": "Beter_UF",
        "limit": {
          "type": "Liability",
          "amount": 300
        },
        "delay": 6
      },
      "isFrozen": false,
      "sourceTimestamp": "2023-10-31T14:21:04.104+00:00"
    },
    {
      "sourceDataVersion": 19,
      "visibility": {
        "default": true,
        "cM1": true,
        "cM3": true
      },
      "key": {
        "eventId": "10579790",
        "tradingType": 1,
        "marketType": 5,
        "period": 0,
        "subPeriod": null,
        "layout": null
      },
      "marketItems": [
        {
          "values": [
            "2.5"
          ],
          "isOpen": true,
          "outcomes": [
            {
              "outcomeType": 4,
              "outcomeValues": [],
              "price": 1.93,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[5,[2.5],[0],1,4,[]]",
              "dataVersion": 9,
              "probability": null,
              "limitPercentage": 1
            },
            {
              "outcomeType": 5,
              "outcomeValues": [],
              "price": 1.77,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[5,[2.5],[0],1,5,[]]",
              "dataVersion": 9,
              "probability": null,
              "limitPercentage": 1
            }
          ],
          "oddsMultipliers": {
            "default": 1,
            "cM1": 1.0481,
            "cM2": 1.0480
          },
          "tradingInfoCustomization": {
            "default": {
              "absoluteLimit": null,
              "delay": null
            },
            "cM1": {
              "absoluteLimit": null,
              "delay": null
            },
            "cM3": {
              "absoluteLimit": null,
              "delay": null
            }
          },
          "isRemoved": false
        },
        {
          "values": [
            "3.5"
          ],
          "isOpen": true,
          "outcomes": [
            {
              "outcomeType": 4,
              "outcomeValues": [],
              "price": 4,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[5,[3.5],[0],1,4,[]]",
              "dataVersion": 8,
              "probability": null,
              "limitPercentage": 1
            },
            {
              "outcomeType": 5,
              "outcomeValues": [],
              "price": 1.2,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[5,[3.5],[0],1,5,[]]",
              "dataVersion": 8,
              "probability": null,
              "limitPercentage": 1
            }
          ],
          "oddsMultipliers": {
            "default": 1,
            "cM1": 1.0481,
            "cM2": 1.0480
          },
          "tradingInfoCustomization": {
            "default": {
              "absoluteLimit": null,
              "delay": null
            },
            "cM1": {
              "absoluteLimit": null,
              "delay": null
            },
            "cM3": {
              "absoluteLimit": null,
              "delay": null
            }
          },
          "isRemoved": false
        }
      ],
      "status": "Opened",
      "stage": "Live",
      "parlaySize": 0,
      "dataVersion": 1,
      "sport": "Football",
      "tradingInfo": {
        "trader": "Beter_UF",
        "limit": {
          "type": "Liability",
          "amount": 300
        },
        "delay": 6
      },
      "isFrozen": false,
      "sourceTimestamp": "2023-10-31T14:21:04.104+00:00"
    },
    {
      "sourceDataVersion": 19,
      "visibility": {
        "default": true,
        "cM1": true,
        "cM3": true
      },
      "key": {
        "eventId": "10579790",
        "tradingType": 1,
        "marketType": 7,
        "period": 0,
        "subPeriod": null,
        "layout": "1"
      },
      "marketItems": [
        {
          "values": [
            "1",
            "1.5"
          ],
          "isOpen": true,
          "outcomes": [
            {
              "outcomeType": 37,
              "outcomeValues": [],
              "price": 2.3,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[7,[1,1.5],[0],1,37,[]]",
              "dataVersion": 8,
              "probability": null,
              "limitPercentage": 0.5
            },
            {
              "outcomeType": 38,
              "outcomeValues": [],
              "price": 1.55,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[7,[1,1.5],[0],1,38,[]]",
              "dataVersion": 8,
              "probability": null,
              "limitPercentage": 0.5
            }
          ],
          "oddsMultipliers": {
            "default": 1,
            "cM1": 1.0481,
            "cM2": 1.0480
          },
          "tradingInfoCustomization": {
            "default": {
              "absoluteLimit": null,
              "delay": null
            },
            "cM1": {
              "absoluteLimit": null,
              "delay": null
            },
            "cM3": {
              "absoluteLimit": null,
              "delay": null
            }
          },
          "isRemoved": false
        }
      ],
      "status": "Opened",
      "stage": "Live",
      "parlaySize": 0,
      "dataVersion": 1,
      "sport": "Football",
      "tradingInfo": {
        "trader": "Beter_UF",
        "limit": {
          "type": "Liability",
          "amount": 300
        },
        "delay": 6
      },
      "isFrozen": false,
      "sourceTimestamp": "2023-10-31T14:21:04.104+00:00"
    },
    {
      "sourceDataVersion": 19,
      "visibility": {
        "default": true,
        "cM1": true,
        "cM3": true
      },
      "key": {
        "eventId": "10579790",
        "tradingType": 1,
        "marketType": 7,
        "period": 0,
        "subPeriod": null,
        "layout": "2"
      },
      "marketItems": [
        {
          "values": [
            "2",
            "0.5"
          ],
          "isOpen": true,
          "outcomes": [
            {
              "outcomeType": 37,
              "outcomeValues": [],
              "price": 1.42,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[7,[2,0.5],[0],1,37,[]]",
              "dataVersion": 3,
              "probability": null,
              "limitPercentage": 0.5
            },
            {
              "outcomeType": 38,
              "outcomeValues": [],
              "price": 2.65,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[7,[2,0.5],[0],1,38,[]]",
              "dataVersion": 3,
              "probability": null,
              "limitPercentage": 0.5
            }
          ],
          "oddsMultipliers": {
            "default": 1,
            "cM1": 1.0481,
            "cM2": 1.0480
          },
          "tradingInfoCustomization": {
            "default": {
              "absoluteLimit": null,
              "delay": null
            },
            "cM1": {
              "absoluteLimit": null,
              "delay": null
            },
            "cM3": {
              "absoluteLimit": null,
              "delay": null
            }
          },
          "isRemoved": false
        }
      ],
      "status": "Opened",
      "stage": "Live",
      "parlaySize": 0,
      "dataVersion": 1,
      "sport": "Football",
      "tradingInfo": {
        "trader": "Beter_UF",
        "limit": {
          "type": "Liability",
          "amount": 300
        },
        "delay": 6
      },
      "isFrozen": false,
      "sourceTimestamp": "2023-10-31T14:21:04.104+00:00"
    },
    {
      "sourceDataVersion": 19,
      "visibility": {
        "default": true,
        "cM1": true,
        "cM3": true
      },
      "key": {
        "eventId": "10579790",
        "tradingType": 1,
        "marketType": 800,
        "period": 0,
        "subPeriod": null,
        "layout": null
      },
      "marketItems": [
        {
          "values": [
            "-0.25"
          ],
          "isOpen": true,
          "outcomes": [
            {
              "outcomeType": 86,
              "outcomeValues": [],
              "price": 1.57,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[800,[-0.25],[0],1,86,[]]",
              "dataVersion": 8,
              "probability": null,
              "limitPercentage": 0.25
            },
            {
              "outcomeType": 87,
              "outcomeValues": [],
              "price": 2.25,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[800,[-0.25],[0],1,87,[]]",
              "dataVersion": 8,
              "probability": null,
              "limitPercentage": 0.25
            }
          ],
          "oddsMultipliers": {
            "default": 1,
            "cM1": 1.0481,
            "cM2": 1.0480
          },
          "tradingInfoCustomization": {
            "default": {
              "absoluteLimit": null,
              "delay": null
            },
            "cM1": {
              "absoluteLimit": null,
              "delay": null
            },
            "cM3": {
              "absoluteLimit": null,
              "delay": null
            }
          },
          "isRemoved": false
        },
        {
          "values": [
            "-0.75"
          ],
          "isOpen": true,
          "outcomes": [
            {
              "outcomeType": 86,
              "outcomeValues": [],
              "price": 2.25,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[800,[-0.75],[0],1,86,[]]",
              "dataVersion": 5,
              "probability": null,
              "limitPercentage": 0.25
            },
            {
              "outcomeType": 87,
              "outcomeValues": [],
              "price": 1.57,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[800,[-0.75],[0],1,87,[]]",
              "dataVersion": 5,
              "probability": null,
              "limitPercentage": 0.25
            }
          ],
          "oddsMultipliers": {
            "default": 1,
            "cM1": 1.0481,
            "cM2": 1.0480
          },
          "tradingInfoCustomization": {
            "default": {
              "absoluteLimit": null,
              "delay": null
            },
            "cM1": {
              "absoluteLimit": null,
              "delay": null
            },
            "cM3": {
              "absoluteLimit": null,
              "delay": null
            }
          },
          "isRemoved": false
        }
      ],
      "status": "Opened",
      "stage": "Live",
      "parlaySize": 0,
      "dataVersion": 1,
      "sport": "Football",
      "tradingInfo": {
        "trader": "Beter_UF",
        "limit": {
          "type": "Liability",
          "amount": 300
        },
        "delay": 6
      },
      "isFrozen": false,
      "sourceTimestamp": "2023-10-31T14:21:04.104+00:00"
    },
    {
      "sourceDataVersion": 19,
      "visibility": {
        "default": true,
        "cM1": true,
        "cM3": true
      },
      "key": {
        "eventId": "10579790",
        "tradingType": 1,
        "marketType": 4,
        "period": 1,
        "subPeriod": null,
        "layout": null
      },
      "marketItems": [
        {
          "values": [
            "-1"
          ],
          "isOpen": true,
          "outcomes": [
            {
              "outcomeType": 86,
              "outcomeValues": [],
              "price": 2.95,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[4,[-1],[1],1,86,[]]",
              "dataVersion": 3,
              "probability": null,
              "limitPercentage": 0.25
            },
            {
              "outcomeType": 87,
              "outcomeValues": [],
              "price": 1.35,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[4,[-1],[1],1,87,[]]",
              "dataVersion": 3,
              "probability": null,
              "limitPercentage": 0.25
            }
          ],
          "oddsMultipliers": {
            "default": 1,
            "cM1": 1.0481,
            "cM2": 1.0480
          },
          "tradingInfoCustomization": {
            "default": {
              "absoluteLimit": null,
              "delay": null
            },
            "cM1": {
              "absoluteLimit": null,
              "delay": null
            },
            "cM3": {
              "absoluteLimit": null,
              "delay": null
            }
          },
          "isRemoved": false
        }
      ],
      "status": "Opened",
      "stage": "Live",
      "parlaySize": 0,
      "dataVersion": 1,
      "sport": "Football",
      "tradingInfo": {
        "trader": "Beter_UF",
        "limit": {
          "type": "Liability",
          "amount": 300
        },
        "delay": 6
      },
      "isFrozen": false,
      "sourceTimestamp": "2023-10-31T14:21:04.104+00:00"
    },
    {
      "sourceDataVersion": 19,
      "visibility": {
        "default": true,
        "cM1": true,
        "cM3": true
      },
      "key": {
        "eventId": "10579790",
        "tradingType": 1,
        "marketType": 6,
        "period": 0,
        "subPeriod": null,
        "layout": null
      },
      "marketItems": [
        {
          "values": [],
          "isOpen": true,
          "outcomes": [
            {
              "outcomeType": 6,
              "outcomeValues": [],
              "price": 1.95,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[6,[],[0],1,6,[]]",
              "dataVersion": 4,
              "probability": null,
              "limitPercentage": 1
            },
            {
              "outcomeType": 7,
              "outcomeValues": [],
              "price": 1.75,
              "status": "Opened",
              "lineItemId": "797a4b6479df4f66a355637dc5028050",
              "selectionKey": "[6,[],[0],1,7,[]]",
              "dataVersion": 4,
              "probability": null,
              "limitPercentage": 1
            }
          ],
          "oddsMultipliers": {
            "default": 1,
            "cM1": 1.0481,
            "cM2": 1.0480
          },
          "tradingInfoCustomization": {
            "default": {
              "absoluteLimit": null,
              "delay": null
            },
            "cM1": {
              "absoluteLimit": null,
              "delay": null
            },
            "cM3": {
              "absoluteLimit": null,
              "delay": null
            }
          },
          "isRemoved": false
        }
      ],
      "status": "Opened",
      "stage": "Live",
      "parlaySize": 0,
      "dataVersion": 1,
      "sport": "Football",
      "tradingInfo": {
        "trader": "Beter_UF",
        "limit": {
          "type": "Liability",
          "amount": 300
        },
        "delay": 6
      },
      "isFrozen": false,
      "sourceTimestamp": "2023-10-31T14:21:04.104+00:00"
    }
  ],
  "isBookedForLive": true,
  "isBookedForPrematch": true,
  "tradingInfos": [
    {
      "lineItemId": "797a4b6479df4f66a355637dc5028050",
      "trader": "Beter_UF",
      "limit": {
        "type": "Liability",
        "amount": 300
      },
      "delay": 6,
      "parlaySize": 0,
      "isCashoutAllowed": true,
      "isOveraskAllowed": true,
      "multibetAmountLimit": null
    }
  ],
  "isFrozen": false,
  "dataVersion": 18,
  "sourceDataVersion": 19,
  "timestamp": "2023-10-31T14:21:04.5282677Z",
  "sourceTimestamp": "2023-10-31T14:21:04.462752Z"
}
```
</details>

## Markets results
<details>
  <summary>Market Result JSON description:</summary>

```json
{
  "eventId": string, // Event string id 
  "results": [
    {
      "key": {
        "eventId": string, // Event string id 
        "tradingType": int, // Type of trading 
        "marketType": int, // Type of market, for detail information please look at document described markets or on metadata service 
        "period": int, // Period of match 
        "subPeriod": nullable int, // Subperiod for match - depends on sport, for some sport like as football this field is null 
      },
      "resultItems": [
        {
          "values": [],
          "outcomes": [
            {
              "outcomeType": int, //id type of outcome
              "outcomeValues": [array of string], //parameters of outcome
              "selectionKey": string, //outcome identificator for bet acceptance,
              "result": string, // type of result 
              "deadHeat": nullable double, // Dead Heat is a rule of distribution of places on the basis of fairness, occurs when more than one athlete or team takes the same place.
              "isRemoved": bool // shows if result item was removed in current update 
            }
          ],
          "isRemoved": bool // shows if outcome item was removed in current update
        }
      ],
      "lineItemId": string, //parent market group for current market, required for bet acceptance, if it empty please look at market item lineItemId
      "sport": string, // market sport,
      "isRemoved": bool // shows if result item was removed in current update
    }
  ],
  "resultExplanation": int, //description of results - templateId (id of trmplate from queue with template notes and params - for example "0:2")
  "dataVersion": int, //version of data entity
  "timestamp": DateTime // date time with time zone of last update
}
```
</details>

<details>
  <summary>Example:</summary>

```json
{
    "id": "d51986ee879f49e99e0597b820a34ff6",
    "name": {
        "en": "USA",
        "uk": "США",
        "uz": "AQSh",
        "vi": "Mỹ",
        "zn": "美国",
        "sw": "USA",
        "my": "USA",
        "ru": "США",
        "pt": "EUA",
        "ro": "SUA",
        "es": "Estados Unidos",
        "ms": "USA",
        "th": "สหรัฐอเมริกา",
        "fa": "ایالات متحده آمریکا",
        "zh": "美国"
    },
    "timestamp": "2022-12-22T20:10:28.7454716Z",
    "dataVersion": 75,
    "slug": "usa",
    "sport": "AmericanFootball"
}
```
</details>
