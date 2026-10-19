# Software Engineering I

## Rest API

### Index

#### Schemas

* [User](#user)
* [Club](#club)
* [Player](#player)
* [Behavior](#behavior)
* [Team](#team)
* [Coordinates](#coordinates)
* [Classification](#classification)
* [Match](#match)
* [Match Detailed](#matchdetailed)
* [League Table Entry](#league_table_entry)
* [League](#league)
* [League Detailed](#leaguedetailed)
* [Friendly Match](#friendlymatch)

#### Paths

* [/users/me](#usersme)
* [/players/](#players)
* [/players/{id_player}/](#playersid_player)
* [/behaviors/](#behaviors)
* [/behaviors/{id_behavior}/](#behaviorsid_behavior)
* [/team/](#team-1)
* [/leagues/](#leagues)
* [/leagues/{id_league}/](#leaguesid_league)
* [/leagues/{id_league}/join](#leaguesid_leaguejoin)
* [/leagues/{id_league}/leave](#leaguesid_leagueleave)
* [/leagues/{id_league}/start](#leaguesid_leaguestart)
* [/leagues/{id_league}/team](#leaguesid_leagueteam)
* [/matches/{id_match}/](#matchesid_match)
* [/friendlymatch/](#friendlymatch-1)
* [/friendlymatch/{id_friendly}/](#friendlymatchid_friendly)
* [/friendlymatch/{id_friendly}/join](#friendlymatchid_friendlyjoin)
* [/friendlymatch/{id_friendly}/leave](#friendlymatchid_friendlyleave)
* [/friendlymatch/{id_friendly}/start](#friendlymatchid_friendlystart)
* [/friendlymatch/{id_friendly}/team](#friendlymatchid_friendlyteam)
* [/history/](#history)
* [/classification/](#classification-1)
* [/auth/register/](#authregister)
* [/auth/login/](#authlogin)
* [/auth/logout/](#authlogout)

---

## Schemas

### User

* id\_user: number
* email: string
* club\_name: string
* avatar: string
* points: number

### Club

* id\_user: number
* club\_name: string  
* avatar: string  

### Player

* id\_player: number
* name: string
* number: number
* strength: number
* power: number
* agility: number
* speed: number
* control: number

### Behavior

* id\_behavior: number
* name: string
* code: string

### Team

* players: [id\_player, id\_player, id\_player]
* behaviors: [id\_behavior, id\_behavior, id\_behavior]
* substitutes: [id\_player, id\_player, id\_player]
* line\_up: "1-1-1" | "2-1" | "1-2"

### Coordinates

* x: number
* y: number

### Classification

* club\_name: string
* points: number

### Match

* id\_match: number
* local: [Club](#club)
* visitor: [Club](#club)
* local\_goals: number
* visitor\_goals: number
* time\_left: number
* status: "pending" | "in\_progress" | "finished"

### MatchDetailed

* id\_match: number
* local: {
  * club: [Club](#club),
  * players: ([Player](#player), [Player](#player), [Player](#player)),
  * behaviors: ([Behavior](#behavior), [Behavior](#behavior), [Behavior](#behavior)),
  * substitutes: ([Player](#player), [Player](#player), [Player](#player)),
  * line\_up: "1-1-1" | "2-1" | "1-2"
* }
* visitor: {
  * club: [Club](#club),
  * players: ([Player](#player), [Player](#player), [Player](#player)),
  * behaviors: ([Behavior](#behavior), [Behavior](#behavior), [Behavior](#behavior)),
  * substitutes: ([Player](#player), [Player](#player), [Player](#player)),
  * line\_up: "1-1-1" | "2-1" | "1-2"
* }
* local\_goals: number
* visitor\_goals: number
* local\_coords: ([Coordinates](#coordinates), [Coordinates](#coordinates), [Coordinates](#coordinates))
* visitor\_coords: ([Coordinates](#coordinates), [Coordinates](#coordinates), [Coordinates](#coordinates))
* ball: [Coordinates](#coordinates)
* time: number
* time\_left: number
* status: "pending" | "in\_progress" | "finished"

### League_table_entry

* club\_name: string
* goals\_scored: number
* goals\_conceded: number
* points: number

### League

* id\_league: number
* is\_private: boolean
* name: string
* match: [Match](#match)
* clubs: list[id\_user]
* max\_clubs: number
* result: number
* time: number
* status: "pending" | "in\_progress" | "finished"

### LeagueDetailed

* id\_league: number
* is\_private: boolean
* name: string
* creator: [Club](#club)
* clubs: list[[Club](#club)]
* matches: list[[Match](#match)]
* table: list[[League_table_entry](#league_table_entry)]
* max\_clubs: number
* time: number
* status: "pending" | "in\_progress" | "finished"

### FriendlyMatch

* id\_friendly: number
* is\_private: boolean
* name: string
* match: [Match](#match)
* result: number
* time: number
* status: "pending" | "in\_progress" | "finished"

---

## Paths

### /users/me

* **GET**:
  * **returns**: [User](#user)
* **PATCH**:
  * **asks**: [Club](#club) (without id)
  * **returns**: [User](#user)
  
### /players/

* **GET**:
  * **returns**: list[[Player](#player)]
* **POST**:
  * **asks**: [Player](#player) (without id)
  * **returns**: [Player](#player)

### /players/{id_player}/

* **GET**:
  * **returns**: [Player](#player)
* **DELETE**:
  * only method

### /behaviors/

* **GET**:
  * **returns**: list[[Behavior](#behavior)]
* **POST**:
  * **asks**: [Behavior](#behavior) (without id)
  * **returns**: [Behavior](#behavior)

### /behaviors/{id_behavior}/

* **GET**:
  * **returns**: [Behavior](#behavior)
* **PATCH**:
  * **asks**: optional[[Behavior](#behavior)] (without id)
  * **returns**: [Behavior](#behavior)
* **DELETE**:
  * only method

### /team/

* **GET**:
  * **returns**: [Team](#team)
* **PATCH**:
  * **asks**: optional[[Team](#team)] (without [Club](#club))
  * **returns**: [Team](#team)

### /leagues/

* **GET**:
  * **parameters**:
    * status: "pending" | "in\_progress" | "finished"
    * friendlies: boolean
    * leagues: boolean
  * **returns**: list[[League](#league)]
* **POST**:
  * **asks**:
    * name: string
    * password?: string
    * is\_friendly: boolean
    * max\_clubs: number
    * time: number
  * **returns**: [LeagueDetailed](#leaguedetailed)

### /leagues/{id_league}/

* **GET**:
  * **returns**: [LeagueDetailed](#leaguedetailed)
* **DELETE**:
  * only method

### /leagues/{id_league}/join

* **POST**:
  * **asks**:
    * password?: string
  * **returns**: [LeagueDetailed](#leaguedetailed)

### /leagues/{id_league}/leave

* **POST**:
  * only method

### /leagues/{id_league}/start

* **POST**:
  * only method

### /leagues/{id_league}/team

* **GET**:
  * **returns**: [Team](#team)
* **PATCH**:
  * **asks**: optional[[Team](#team)] (without [Club](#club))
  * **returns**: [Team](#team)

### /matches/{id_match}/

* **GET**:
  * **returns**: [MatchDetailed](#matchdetailed)

### /friendlymatch/

* **GET**:
  * **parameters**:
    * status: "pending" | "in\_progress" | "finished"
  * **returns**: list[[FriendlyMatch](#friendlymatch)]
* **POST**:
  * **asks**:
    * name: string
    * password?: string
    * time: number
  * **returns**: [FriendlyMatch](#friendlymatch)

### /friendlymatch/{id_friendly}/

* **GET**:
  * **returns**: [FriendlyMatch](#friendlymatch)
* **DELETE**:
  * only method

### /friendlymatch/{id_friendly}/join

* **POST**:
  * **asks**:
    * password?: string
  * **returns**: [FriendlyMatch](#friendlymatch)

### /friendlymatch/{id_friendly}/leave

* **POST**:
  * only method

### /friendlymatch/{id_friendly}/start

* **POST**:
  * only method

### /friendlymatch/{id_friendly}/team

* **GET**:
  * **returns**: [Team](#team)
* **PATCH**:
  * **asks**: optional[[Team](#team)] (without [Club](#club))
  * **returns**: [Team](#team)

### /history/

* **GET**:
  * **returns**: list[[Match](#match) | [League](#league)]

### /classification/

* **GET**:
  * **returns**: list[[Classification](#classification)]

### /auth/register/

* **POST**:
  * **asks**:
    * email: string
    * password: string
  * **returns**:
    * token: string
    * [User](#user)

### /auth/login/

* **POST**:
  * **asks**:
    * email: string
    * password: string
  * **returns**:
    * token: string
    * [User](#user)

### /auth/logout/

* **POST**:
  * only method

---

## WebSocket API

### Index

#### Screens

* [Leagues List Screen](#leagues-list-screen)
  * [leagues:add](#leaguesadd)
  * [leagues:update:match](#leaguesupdatematch)
  * [leagues:update:match:goals](#leaguesupdatematchgoals)
  * [leagues:update:match:status](#leaguesupdatematchstatus)
  * [leagues:update:status](#leaguesupdatestatus)
  * [leagues:update:club:add](#leaguesupdateclubadd)
  * [leagues:update:club:delete](#leaguesupdateclubdelete)
  * [leagues:delete](#leaguesdelete)
* [League Screen](#league-screen)
  * [league:status](#leaguestatus)
  * [league:delete](#leaguedelete)
  * [league:club:add](#leagueclubadd)
  * [league:club:delete](#leagueclubdelete)
  * [league:table](#leaguetable)
  * [league:match:goals](#leaguematchgoals)
  * [league:match:status](#leaguematchstatus)
* [Match Screen](#match-screen)
  * [match:update](#matchupdate)
  * [match:goals](#matchgoals)
  * [match:break](#matchbreak)
  * [client:match:substitutes](#clientmatchsubstitutes)
  * [client:match:behaviors](#clientmatchbehaviors)
  * [match:status](#matchstatus)

---

## Screens

### Leagues List Screen

* <a id="leaguesadd"></a>**leagues:add** *(SERVER -> CLIENT)*:
  * Esquemas relacionados: [League](#league)

```json
  {
    "type": "leagues:add",
    "league": League
  }
```

> *Update match completo*

* <a id="leaguesupdatematch"></a>**leagues:update:match** *(SERVER -> CLIENT)*:
  * Esquemas relacionados: [Match](#match)

```json
  {
    "type": "leagues:update:match",
    "id_league": number,
    "match": Match
  }
```

> *Update match en vivo*

* <a id="leaguesupdatematchgoals"></a>**leagues:update:match:goals** *(SERVER -> CLIENT)*:

```json
  {
    "type": "leagues:update:match:goals",
    "id_league": number,
    "local_goals": number,
    "visitor_goals": number
  }
```

* <a id="leaguesupdatematchstatus"></a>**leagues:update:match:status** *(SERVER -> CLIENT)*:

```json
  {
    "type": "leagues:update:match:status",
    "id_league": number,
    "status": "pending" | "in_progress" | "finished"
  }
```

> *Update league*

* <a id="leaguesupdatestatus"></a>**leagues:update:status** *(SERVER -> CLIENT)*:

```json
  {
    "type": "leagues:update:status",
    "id_league": number,
    "result": number,
    "status": "pending" | "in_progress" | "finished"
  }
```

* <a id="leaguesupdateclubadd"></a>**leagues:update:club:add** *(SERVER -> CLIENT)*:

```json
  {
    "type": "leagues:update:club:add",
    "id_league": number,
    "id_user": number
  }
```

* <a id="leaguesupdateclubdelete"></a>**leagues:update:club:delete** *(SERVER -> CLIENT)*:

```json
  {
    "type": "leagues:update:club:delete",
    "id_league": number,
    "id_user": number
  }
```

* <a id="leaguesdelete"></a>**leagues:delete** *(SERVER -> CLIENT)*:

```json
  {
    "type": "leagues:delete",
    "id_league": number
  }
```

### League Screen

* <a id="leaguestatus"></a>**league:status** *(SERVER -> CLIENT)*:

```json
  {
    "type": "league:status",
    "status": "pending" | "in_progress" | "finished"
  }
```

> *Pending league*

* <a id="leaguedelete"></a>**league:delete** *(SERVER -> CLIENT)*:

```json
  {
    "type": "league:delete"
  }
```

* <a id="leagueclubadd"></a>**league:club:add** *(SERVER -> CLIENT)*:
  * Esquemas relacionados: [Club](#club)

```json
  {
    "type": "league:club:add",
    "club": Club
  }
```

* <a id="leagueclubdelete"></a>**league:club:delete** *(SERVER -> CLIENT)*:

```json
  {
    "type": "league:club:delete",
    "id_club": number
  }
```

> *In-progress league*

* <a id="leaguetable"></a>**league:table** *(SERVER -> CLIENT)*:
  * Esquemas relacionados: [League Table Entry](#league_table_entry)

```json
  {
    "type": "league:table",
    "table": list[League_table_entry]
  }
```

* <a id="leaguematchgoals"></a>**league:match:goals** *(SERVER -> CLIENT)*:

```json
  {
    "type": "league:match:goals",
    "id_match": number,
    "local_goals": number,
    "visitor_goals": number
  }
```

* <a id="leaguematchstatus"></a>**league:match:status** *(SERVER -> CLIENT)*:

```json
  {
    "type": "league:match:status",
    "id_match": number,
    "status": "pending" | "in_progress" | "finished"
  }
```

### Match Screen

* <a id="matchupdate"></a>**match:update** *(SERVER -> CLIENT)*:
  * Esquemas relacionados: [Coordinates](#coordinates)

```json
  {
    "type": "match:update",
    "local_coords": (Coordinates, Coordinates, Coordinates), // players positions
    "visitor_coords": (Coordinates, Coordinates, Coordinates), // players positions
    "ball": Coordinates,
    "time_left": number
  }
```

* <a id="matchgoals"></a>**match:goals** *(SERVER -> CLIENT)*:

```json
  {
    "type": "match:goals",
    "local_goals": number,
    "visitor_goals": number
  }
```

> *Cambia a jugadores titulares y suplentes*

* <a id="matchbreak"></a>**match:break** *(SERVER -> CLIENT)*:

```json
  {
    "type": "match:break",
    "local": (id_player, id_player, id_player),
    "visitor": (id_player, id_player, id_player)
  }
```

* <a id="clientmatchsubstitutes"></a>**client:match:substitutes** *(CLIENT -> SERVER)*:

```json
  {
    "type": "client:match:substitutes",
    "players": (id_player, id_player, id_player)
  }
```

* <a id="clientmatchbehaviors"></a>**client:match:behaviors** *(CLIENT -> SERVER)*:

```json
  {
    "type": "client:match:behaviors",
    "behaviors": (id_behavior, id_behavior, id_behavior)
  }
```

* <a id="matchstatus"></a>**match:status** *(SERVER -> CLIENT)*:

```json
  {
    "type": "match:status",
    "status": "pending" | "in_progress" | "finished"
  }
```
