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

#### Paths

* [/users/me](#usersme)
* [/players/](#players)
* [/players/{player_id}/](#playersplayer_id)
* [/behaviors/](#behaviors)
* [/behaviors/{behavior_id}/](#behaviorsbehavior_id)
* [/team/](#team-1)
* [/leagues/](#leagues)
* [/leagues/{league_id}/](#leaguesleague_id)
* [/leagues/{league_id}/join](#leaguesleague_idjoin)
* [/leagues/{league_id}/leave](#leaguesleague_idleave)
* [/leagues/{league_id}/start](#leaguesleague_idstart)
* [/leagues/{league_id}/team](#leaguesleague_idteam)
* [/leagues/{league_id}/matches/{match_id}/](#leaguesleague_idmatchesmatch_id)
* [/history/](#history)
* [/classification/](#classification-1)
* [/auth/register/](#authregister)
* [/auth/login/](#authlogin)
* [/auth/logout/](#authlogout)

---

## Schemas

### User

* user\_id: number
* email: string
* username: string
* club\_name: string
* avatar: string
* points: number

### Club

* club\_id: number
* name: string  
* avatar: string  

### Player

* player\_id: number
* name: string
* number: number
* strength: number
* power: number
* agility: number
* speed: number
* control: number

### Behavior

* behavior\_id: number
* name: string
* code: string

### Team

* club: [Club](#club)
* players: ([Player](#player), [Player](#player), [Player](#player))
* behaviors: ([Behavior](#behavior), [Behavior](#behavior), [Behavior](#behavior))
* substitutes: ([Player](#player), [Player](#player), [Player](#player))
* line\_up: "1-1-1" | "2-1" | "1-2"

### Coordinates

* x: number
* y: number

### Classification

* club\_name: string
* points: number

### Match

* match\_id: number
* local: [Club](#club)
* visitor: [Club](#club)
* local\_goals: number
* visitor\_goals: number
* time\_left: number
* status: "pending" | "in\_progress" | "finished"

### MatchDetailed

* match\_id: number
* local: [Team](#team)
* visitor: [Team](#team)
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

* league\_id: number
* is\_private: boolean
* is\_friendly: boolean
* name: string
* match: [Match](#match)
* clubs\_count: number
* max\_clubs: number
* result: number
* time: number
* status: "pending" | "in\_progress" | "finished"

### LeagueDetailed

* league\_id: number
* is\_private: boolean
* name: string
* creator: [Club](#club)
* clubs: list[[Club](#club)]
* matches: list[[Match](#match)]
* table: list[[League_table_entry](#league_table_entry)]
* max\_clubs: number
* time: number
* status: "pending" | "in\_progress" | "finished"

---

## Paths

### /users/me

* **GET**:
  * **returns**: [User](#user)
* **PUT**:
  * **asks**: [Club](#club) (without id)
  * **returns**: [User](#user)
  
### /players/

* **GET**:
  * **returns**: list[[Player](#player)]
* **POST**:
  * **asks**: [Player](#player) (without id)
  * **returns**: [Player](#player)

### /players/{player_id}/

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

### /behaviors/{behavior_id}/

* **GET**:
  * **returns**: [Behavior](#behavior)
* **PUT**:
  * **asks**: optional[[Behavior](#behavior)] (without id)
  * **returns**: [Behavior](#behavior)
* **DELETE**:
  * only method

### /team/

* **GET**:
  * **returns**: [Team](#team)
* **PUT**:
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

### /leagues/{league_id}/

* **GET**:
  * **returns**: [LeagueDetailed](#leaguedetailed)
* **DELETE**:
  * only method

### /leagues/{league_id}/join

* **POST**:
  * **asks**:
    * password?: string
  * **returns**: [LeagueDetailed](#leaguedetailed)

### /leagues/{league_id}/leave

* **POST**:
  * only method

### /leagues/{league_id}/start

* **POST**:
  * only method

### /leagues/{league_id}/team

* **GET**:
  * **returns**: [Team](#team)
* **PUT**:
  * **asks**: optional[[Team](#team)] (without [Club](#club))
  * **returns**: [Team](#team)

### /leagues/{league_id}/matches/{match_id}/

* **GET**:
  * **returns**: [MatchDetailed](#matchdetailed)

### /history/

* **GET**:
  * **returns**: list[[Match](#match) | [League](#league)]

### /classification/

* **GET**:
  * **returns**: list[[Classification](#classification)]

### /auth/register/

* **POST**:
  * **asks**:
    * username: string
    * name: string
    * password: string
  * **returns**:
    * token: string
    * [User](#user)

### /auth/login/

* **POST**:
  * **asks**:
    * username: string
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
  * [leagues:update:clubs_count](#leaguesupdateclubs_count)
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
  ```jsonc
  {
    "type": "leagues:add",
    "league": League
  }
  ```

> *Update match completo*

* <a id="leaguesupdatematch"></a>**leagues:update:match** *(SERVER -> CLIENT)*:
  * Esquemas relacionados: [Match](#match)
  ```jsonc
  {
    "type": "leagues:update:match",
    "league_id": number,
    "match": Match
  }
  ```

> *Update match en vivo*

* <a id="leaguesupdatematchgoals"></a>**leagues:update:match:goals** *(SERVER -> CLIENT)*:
  ```jsonc
  {
    "type": "leagues:update:match:goals",
    "league_id": number,
    "local_goals": number,
    "visitor_goals": number
  }
  ```

* <a id="leaguesupdatematchstatus"></a>**leagues:update:match:status** *(SERVER -> CLIENT)*:
  ```jsonc
  {
    "type": "leagues:update:match:status",
    "league_id": number,
    "status": "pending" | "in_progress" | "finished"
  }
  ```

> *Update league*

* <a id="leaguesupdatestatus"></a>**leagues:update:status** *(SERVER -> CLIENT)*:
  ```jsonc
  {
    "type": "leagues:update:status",
    "league_id": number,
    "result": number,
    "status": "pending" | "in_progress" | "finished"
  }
  ```

* <a id="leaguesupdateclubs_count"></a>**leagues:update:clubs_count** *(SERVER -> CLIENT)*:
  ```jsonc
  {
    "type": "leagues:update:clubs_count",
    "league_id": number,
    "clubs_count": number
  }
  ```

* <a id="leaguesdelete"></a>**leagues:delete** *(SERVER -> CLIENT)*:
  ```jsonc
  {
    "type": "leagues:delete",
    "league_id": number
  }
  ```

### League Screen

* <a id="leaguestatus"></a>**league:status** *(SERVER -> CLIENT)*:
  ```jsonc
  {
    "type": "league:status",
    "status": "pending" | "in_progress" | "finished"
  }
  ```

> *Pending league*

* <a id="leaguedelete"></a>**league:delete** *(SERVER -> CLIENT)*:
  ```jsonc
  {
    "type": "league:delete"
  }
  ```

* <a id="leagueclubadd"></a>**league:club:add** *(SERVER -> CLIENT)*:
  * Esquemas relacionados: [Club](#club)
  ```jsonc
  {
    "type": "league:club:add",
    "club": Club
  }
  ```

* <a id="leagueclubdelete"></a>**league:club:delete** *(SERVER -> CLIENT)*:
  ```jsonc
  {
    "type": "league:club:delete",
    "club_id": number
  }
  ```

> *In-progress league*

* <a id="leaguetable"></a>**league:table** *(SERVER -> CLIENT)*:
  * Esquemas relacionados: [League Table Entry](#league_table_entry)
  ```jsonc
  {
    "type": "league:table",
    "table": list[League_table_entry]
  }
  ```

* <a id="leaguematchgoals"></a>**league:match:goals** *(SERVER -> CLIENT)*:
  ```jsonc
  {
    "type": "league:match:goals",
    "match_id": number,
    "local_goals": number,
    "visitor_goals": number
  }
  ```

* <a id="leaguematchstatus"></a>**league:match:status** *(SERVER -> CLIENT)*:
  ```jsonc
  {
    "type": "league:match:status",
    "match_id": number,
    "status": "pending" | "in_progress" | "finished"
  }
  ```

### Match Screen

* <a id="matchupdate"></a>**match:update** *(SERVER -> CLIENT)*:
  * Esquemas relacionados: [Coordinates](#coordinates)
  ```jsonc
  {
    "type": "match:update",
    "local_coords": (Coordinates, Coordinates, Coordinates), // players positions
    "visitor_coords": (Coordinates, Coordinates, Coordinates), // players positions
    "ball": Coordinates,
    "time_left": number
  }
  ```

* <a id="matchgoals"></a>**match:goals** *(SERVER -> CLIENT)*:
  ```jsonc
  {
    "type": "match:goals",
    "local_goals": number,
    "visitor_goals": number
  }
  ```

> *Cambia a jugadores titulares y suplentes*

* <a id="matchbreak"></a>**match:break** *(SERVER -> CLIENT)*:
  * Esquemas relacionados: [Player](#player)
  ```jsonc
  {
    "type": "match:break",
    "local": (player_id, player_id, player_id),
    "visitor": (player_id, player_id, player_id)
  }
  ```

* <a id="clientmatchsubstitutes"></a>**client:match:substitutes** *(CLIENT -> SERVER)*:
  * Esquemas relacionados: [Player](#player)
  ```jsonc
  {
    "type": "client:match:substitutes",
    "players": (player_id, player_id, player_id)
  }
  ```

* <a id="clientmatchbehaviors"></a>**client:match:behaviors** *(CLIENT -> SERVER)*:
  * Esquemas relacionados: [Behavior](#behavior)
  ```jsonc
  {
    "type": "client:match:behaviors",
    "behaviors": (behavior_id, behavior_id, behavior_id)
  }
  ```

* <a id="matchstatus"></a>**match:status** *(SERVER -> CLIENT)*:
  ```jsonc
  {
    "type": "match:status",
    "status": "pending" | "in_progress" | "finished"
  }
  ```

