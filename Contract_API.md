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
* [Match](#match)

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

* club: Club
* players: (Player, Player, Player)
* behaviors: (Behavior, Behavior, Behavior)
* substitutes: (Player, Player, Player)
* line\_up: "1-1-1" | "2-1" | "1-2"

### Coordinates

* x: number
* y: number

### Classification

* club\_name: string
* points: number

### Match

* match\_id: number
* local: Club
* visitor: Club
* local\_goals: number
* visitor\_goals: number
* time\_left: number
* status: "pending" | "in\_progress" | "finished"

### MatchDetailed

* match\_id: number
* local: Team
* visitor: Team
* local\_goals: number
* visitor\_goals: number
* local\_coords: (Coordinates, Coordinates, Coordinates)
* visitor\_coords: (Coordinates, Coordinates, Coordinates)
* ball: Coordinates
* time: number
* time\_left: number
* status: "pending" | "in\_progress" | "finished"

### League\_table\_entry

* club\_name: string
* goals\_scored: number
* goals\_conceded: number
* points: number

### League

* league\_id: number
* is\_private: boolean
* is\_friendly: boolean
* name: string
* match: Match
* clubs\_count: number
* max\_clubs: number
* result: number
* time: number
* status: "pending" | "in\_progress" | "finished"

### LeagueDetailed

* league\_id: number
* is\_private: boolean
* name: string
* creator: Club
* clubs: Club\[\]
* matches: Match\[\]
* table: list\[League\_table\_entry\]
* max\_clubs: number
* time: number
* status: "pending" | "in\_progress" | "finished"

---

## Paths

### /users/me

    GET:
        returns:
            User
    PUT:
        asks:
            Club (without id)
        returns:
            User

### /players/

    GET:
        returns:
            list[Player]
    POST:
        asks:
            Player (without id)
        returns:
            Player

### /players/{player_id}/

    GET:
        returns:
            Player
    DELETE:
        only method

### /behaviors/

    GET:
        returns:
            list[Behavior]
    POST:
        asks:
            optional[Behavior]  (without id)
        returns:
            Behavior

### /behaviors/{behavior_id}/

    GET:
        returns:
            Behavior
    PUT:
        asks:
            optional[Behavior] (without id)
        returns:
            Behavior
    DELETE:
        only method

### /team/

    GET:
        returns:
            Team
    PUT:
        asks:
            optional[Team] (without Club)
        returns:
            Team

### /leagues/

    GET:
        parameters:
            status: "pending" | "in\_progress" | "finished"
            friendlies: boolean
            leagues: boolean
        returns:
            list[League]
    POST:
        asks:
            name: string
            password?: string
            is\_friendly: boolean
            max\_clubs: number
            time: number
        returns:
            LeagueDetailed

### /leagues/{league_id}/

    GET:
        returns:
            LeagueDetailed
    DELETE:
        only method

### /leagues/{league_id}/join

    POST:
        asks:
            password?: string
        returns:
            LeagueDetailed

### /leagues/{league_id}/leave

    POST:
        only method

### /leagues/{league_id}/start

    POST:
        only method

### /leagues/{league_id}/team

    GET:
        returns:
            Team
    POST:
        asks:
            optional[Team] (without Club)
        returns:
            Team

### /leagues/{league_id}/matches/{match_id}/

    GET:
        returns:
            MatchDetailed

### /history/

    GET:
        returns:
            list[Match | League]

### /classification/

    GET:
        returns:
            list[Classification]

### /auth/register/

    POST:
        asks:
            username: string
            name: string
            password: string
        returns:
            token: string
            User

### /auth/login/

    POST:
        asks:
            username:string
            password: string
        returns:
            token: string
            User

### /auth/logout/

    POST:
        only method
