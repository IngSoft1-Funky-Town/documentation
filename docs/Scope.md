# Software Engineering I

## Project Scope

### Index

1. [General objective](#general-objective)
2. [Principal features](#principal-features)
3. [Functional requirements](#functional-requirements)
    1. [Authentication and User Management](#authentication-and-user-management)
    2. [DT Management (Players and behaviors)](#dt-management-players-and-behaviors)
    3. [League and Match Management](#league-and-match-management)
4. [Out of Scope](#out-of-scope)
5. [Possible extensions](#possible-extensions)

---

## General objective

The objective is to develop a football club management system with match simulation where the user can register and manage their own football club. In addition, create players and their custom behaviors and play leagues or friendly matches with other users.

## Principal features

The site will provide users with the following fundamental capabilities:

1. Squad management: The ability to manage the player roster and their possible behaviors.
2. Competition System: The ability to create and participate in public and private leagues, as well as to organize friendly matches.
3. Live Simulation and Interaction: Real-time match visualization and tactical decision-making.

### Functional requirements

#### Authentication and User Management

* The system shall allow users to register on the platform, which will need to fill all information needed for the account.
* The system shall allow the user to log in and log out.
* The user will be able to edit basic club information (such as name or badge).
* The user will be able to navigate their profile.
* The user will be able to consult their play history, showing for each past match the date, result(victory/defeat), opponent and the name of the league in case it was a league match.

#### DT Management (Players and behaviors)

* The user will be able to create new players for their squad and delete existing players.
* The user will be able to create, modify, or delete tactical behaviors using Python code.
* The system shall verify that the uploaded behavior code is syntactically valid and executes without errors, and shall run a security check on it.
* The system shall notify the user whether their code is authorized for use.
* The user will be able to edit their default team (configuring which players ,behaviors and kickoff lineup are used by default).
* The user will be able to edit this default team specifically when registering their club for a league or friendly match (with the option to leave it unmodified).

#### League and Match Management

* The user will be able to view a list of their current activity (ongoing leagues and matches they are involved in).
* **Leagues:**
  * The system shall allow users to create a league and navigate available leagues.
  * Users will be able to join a public or private league.
  * The user will be able to leave a league they joined, as long as it has not started yet.
  * The user who created a league will be able to cancel a league before it starts.
  * The user who created a league will be the only one able to start the league once the minimum number of participants is reached, which locks registration and generates the fixture.
  * The user will be able to navigate an active league's.
  * The system will break ties between users that have the same points in the league using in order goals difference, goals in favor, goals conceded and match results between them.
* **Friendly Matches:**
  * The user will be able to create a friendly match and navigate available friendly matches.
  * The user will be able to join a public or private friendly match.
  * The user will be able to leave a friendly match, as long as it has not started yet.
  * The friendly match creator will be able to cancel the friendly match before it starts.
  * The friendly match creator will be able to start the friendly match.
* **Match Execution:**
  * Users will be able to make tactical decisions by viewing the live state of the match being simulated by the system.
  * The system shall send the match status to the user every time a tick is calculated.
  * Users will be able to play against the default squad of another club if the other user doesn't connect.
  * Users will be able to leave the view of an ongoing match. The match will continue in progress with the team's current players and behaviors.
  * The user will be able to re-enter a match they previously left, as long as it is still in progress.
  * The user will be able to enter a match as a spectator(without control privileges).
  * The user will be able to change a first team player's active behavior in real time during the match. The change is applied on the next simulation tick.
  * The user will be able to call for a substitution during a cooling break or half-time, exchanging any number of bench players for field players(maximum of three players).
* **Ranking:**
  * Users will be able to consult a global world ranking of clubs, calculated only from public league matches and friendly matches, where private matches cannot be used to inflate a club's standing.

### Out of Scope

* Users will not be able to upload custom badges, they may only select from a list of logos already available in the system.
* Users will not be able to edit an existing player's attributes once created (they may only delete and re-create a player).
* Users will not be able to delete players or behaviors if they are linked to a league or the default squad.
* There will be no chat feature.

### Possible extensions

* The user may assign a default squad to each formation.
* The league creator may remove a user from the league.
