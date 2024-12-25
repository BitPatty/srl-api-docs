# (Unofficial) SpeedRunsLive API Documentation

This documentation is based on endpoints found while inspecting the SRL pages. This page only covers API endpoints from the new API (since the one at api.speedrunslive.com might be shut down soonish). The new API base is available at https://speedrunslive.com/api.

## Live Streams

### GET /api/livestreams

Returns the list of livestreams displayed on the home page.

```jsonc
{
    "data": [
        {
            "id": "12345678912",
            "game": "Grand Theft Auto V",
            "name": "SomeTwitchUserName",
            "playerName": "SomeSRLUserName",
            "profileImage": "https://...",
            "title": "Some Stream Title",
            "viewercount": 1234
        },
        {
            /* ... */
        }
    ]
}
```

## Races

### GET /api/currentraces

Returns a paginated list of active races.

#### Params

| Param        | Description         |
|--------------|---------------------|
| `pageNumber` | The page to display |
| `pageSize`   | The page size       |

#### Sample Output

```jsonc
{
    "data": [
        {
            "currentRaceFileName": ???,
            "currentRaceGameId": 6222,
            "currentRaceGoal": "Tower of Oannes",
            "currentRaceId": "or4bu",
            "currentRaceState": 3,
            "currentRaceStateText": "In Progress",
            "currentRaceTime": "2022-01-28T23:50:03+00:00",
            "elapsedTime": 1234,
            "entrants": [
                {
                    "currentRaceLinkId": 12345,
                    "currentRacePlayerId": 123,
                    "currentRacePlayerName": "SomeSRLUserName",
                    "message": "",
                    "place": 1234,
                    "rating": 0,
                    "time": -3
                }
                {
                    /* ... */
                }
            ],
            "game": {
                "gameAbbrev": "lamulana2",
                "gameName": "La-Mulana 2",
                "gamePopularity": 0,
                "isSeasonGame": false
            },
            "totalEntrants": 2
        },
        {
            /* ... */
        }
    ],
    "pageNumber": 1,
    "pageSize": 12,
    "totalPages": 2
}
```

### GET /api/currentraces/&lt;race-id&gt;

Returns the info of a single race, same data as GET /api/currentraces -> data.

## Past Races

### GET /api/pastresults

Returns a paginated list of race results.

#### Params

| Param        | Description                           |
|--------------|---------------------------------------|
| `player`     | Filter results by a player name       |
| `game`       | Filter results by a game abbreviation |
| `pageNumber` | The page to display                   |
| `pageSize`   | The page size                         |

## Games

### GET /api/games

Returns a paginated list of games.

#### Params

| Param        | Description                                       |
|--------------|---------------------------------------------------|
| `pageNumber` | The page to display                               |
| `pageSize`   | The page size                                     |
| `sortBy`     | If set to `popularity`, sorty by popularity score |
| `orderBy`    | Either `asc` for ascending or `desc`              |

#### Sample Output

```jsonc
{
    "data": [
        {
            "gameAbbrev": "sm64",
            "gameName": "Super Mario 64",
            "gamePopularity": 974,
            "isSeasonGame": false
        },
        {
            /* ... */
        }
    ],
    "pageNumber": 1,
    "pageSize": 20,
    "totalPages": 322
}
```

## Statistics

### GET /api/stats/all

Returns the overall SRL race statistics.

#### Sample Output

```jsonc
{
    "data":{
        "totalRaces":286503,
        "totalPlayers":36165,
        "totalGames":6426,
        "largestRaceId":125224,
        "largestRaceSize":301,
        "totalRaceTime":1374617114,
        "totalPlayedTime":3998093958
    }
}
```

### GET /api/stats/monthly

Returns the monthly race statistics.

#### Sample Output

```jsonc
{
    "data":[
        {
            "year":2022,
            "months":[
                {
                    "month":1,
                    "totalRaces":180,
                    "totalPlayers":185,
                    "totalGames":127,
                    "largestRace":286579,
                    "totalRaceTime":180,
                    "totalTimePlayed":1737482,
                    "largestRaceSize":16
                }
            ]
        },
        {
            /* ... */
        }
    ],
    "totalPages":0,
    "pageNumber":0,
    "pageSize":12
}
```

### GET /api/stats/players

Returns a paginated list of race stats grouped by user.

#### Params

| Param        | Description         |
|--------------|---------------------|
| `pageNumber` | The page to display |
| `pageSize`   | The page size       |

#### Sample Output

```jsonc
{
    "data":[
        {
            "playerId":147,
            "playerName":"neskamikaze",
            "totalRaces":3769,
            "totalGames":1312,
            "firstRaceId":1731,
            "firstRaceDate":"2011-02-16T00:55:53+00:00",
            "totalPlayedTime":9057577,
            "totalFirsts":1560,
            "totalSeconds":1102,
            "totalThirds":320,
            "totalQuits":347,
            "totalDQs":5
        },
        {
            /* ... */
        }
    ],
    "totalPages":0,
    "pageNumber":0,
    "pageSize":12
}
```

### GET /api/stats/players/&lt;player-name&gt;

Returns the race stats of the specified user.

#### Sample Output

```jsonc
{
    "data": {
        "playerId":19075,
        "playerName":"psychonauter",
        "totalRaces":55,
        "totalGames":2,
        "firstRaceId":167799,
        "firstRaceDate":"2016-04-12T21:25:49+00:00",
        "totalPlayedTime":449503,
        "totalFirsts":11,
        "totalSeconds":5,
        "totalThirds":8,
        "totalQuits":10,
        "totalDQs":0
    }
}
```


### GET /api/stats/playergamestats

Returns the race stats of the specified user in the specified game.

#### Params

| Param        | Description                      |
|--------------|----------------------------------|
| `playerName` | (Required) The user name         |
| `gameAbbrev` | (Required) The game abbreviation |


#### Sample Output

```jsonc
{
    "data":{
        "playerId":19075,
        "gameId":0,
        "totalRaces":48,
        "firstRaceId":167799,
        "firstRaceDate":"2016-04-12T21:25:49+00:00",
        "totalPlayedTime":196639,
        "totalFirsts":8,
        "totalSeconds":5,
        "totalThirds":6,
        "totalQuits":9,
        "totalDQs":0
    }
}
```

### GET /api/bestracetimes/&lt;game-abbreviation&gt;

Returns the top races of the specified game.

#### Sample Output

```jsonc
{
    "data": [
        {
            "goalId": 123,
            "goalName": "16 star",
            "bestTimes": [
                {
                    "raceId": 1234,
                    "playerId": 12345,
                    "time": 123,
                    "playerName": "SomeSRLUserName"
                }
            ]
        }
    ],
    "totalPages": 0,
    "pageNumber": 0,
    "pageSize": 12
}
```

## Players

### GET /api/players

Returns a paginated list of SRL players

#### Params

| Param        | Description         |
|--------------|---------------------|
| `pageNumber` | The page to display |
| `pageSize`   | The page size       |

#### Sample Output

```jsonc
{
    "data": [
        {
            "playerId": 123,
            "playerName": "SomeSRLUserName",
            "roleId": 5,
            "youtube": "",
            "countryName": "",
            "twitter": "",
            "channel" ""
        },
        {
            /* ... */
        }
    ],
    "totalPages": 3014,
    "pageNumber": 1,
    "pageSize": 12
}

```

### GET /api/players/&lt;player-name&gt;

Returns the info of the specified user.

#### Sample Output

```jsonc
{
    "data":{
        "playerId":19075,
        "playerName":"psychonauter",
        "roleId":5,
        "youtube":"",
        "countryName":"Switzerland",
        "twitter":"psychonauter",
        "channel":"psychonauter",
        "playerPlayedGames":[
            {
                "playerId":19075,
                "gameId":7,
                "gameName":"Super Mario Sunshine",
                "gameAbbrev":"sms",
                "totalRaces":48,
                "gameRank":230
            },
            {
                "playerId":19075,
                "gameId":941,
                "gameName":"Final Fantasy X",
                "gameAbbrev":"ffx",
                "totalRaces":7,
                "gameRank":4
            }
        ]
    }
}
```

#### Sample Output

```jsonc
{
    "data":[
        {
            "raceId":267156,
            "raceGoal":"Any%",
            "raceDate":1578331429,
            "seasonId":0,
            "game":{
                "gameName":"Super Mario Sunshine",
                "gameAbbrev":"sms",
                "gamePopularity":153,
                "isSeasonGame":false
            },
            "entrants":[
                {
                    "playerName":"_1UpsForLife",
                    "place":1,
                    "placeText":"",
                    "time":4882,
                    "message":"first weekly of the decade!",
                    "oldRating":720,
                    "newRating":735
                },
                {
                    /* ... */
                }
            ]
        }
    ],
    "totalPages":48,
    "pageNumber":1,
    "pageSize":1
}
```

## Countries

### GET /api/countries

Returns the list of countries available on SRL.

#### Sample Output

```jsonc
{
    "data": [
        {
            "countryId": 1,
            "countryName": "None"
        },
        {
            /* ... */
        }
    ]
}

```

## User / Auth

### POST /api/auth/login

Authenticates a user, returns a cookie called `auth_cookie` used for privileged actions.

#### Payload

```jsonc
{
    "username": "",
    "password": ""
}
```

### POST /api/auth/logout

Allows users to log out, removes the `auth_cookie`.

### GET /api/user/profile

Returns the profile information of the currently authenticated user.

#### Sample Output

```jsonc
{
    "data":{
        "playerName":"psychonauter",
        "twitch":"psychonauter",
        "youtube":"",
        "twitter":"psychonauter",
        "country":"Switzerland",
        "countryId":191,
        "frontPagePref":2
    }
}
```

### PUT /api/user/profile

Updates the profile information of the currently authenticated user.

#### Payload

```jsonc
{
    "playerName":"psychonauter",
    "twitch":"psychonauter",
    "youtube":"",
    "twitter":"psychonauter",
    "countryId":191,
    "frontPagePref":"2"
}
```