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
  * **asks**: optional[[Behavior](#behavior)] (without id)
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
* **POST**:
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
