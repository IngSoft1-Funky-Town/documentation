# Software Engineering I

## Use Cases

### Index

* [UC-01: User registration](#uc-01-user-registration)
* [UC-02: User login](#uc-02-user-login)
* [UC-03: User logout](#uc-03-user-logout)
* [UC-04: Navigate profile](#uc-04-navigate-profile)
* [UC-05: Edit club](#uc-05-edit-club)
* [UC-06: Create player](#uc-06-create-player)
* [UC-07: Delete player](#uc-07-delete-player)
* [UC-08: Create behavior](#uc-08-create-behavior)
* [UC-09: Edit behavior](#uc-09-edit-behavior)
* [UC-10: Delete behavior](#uc-10-delete-behavior)
* [UC-11: Create default team](#uc-11-create-default-team)
* [UC-12: Create league](#uc-12-create-league)
* [UC-13: Navigate leagues](#uc-13-navigate-leagues)
* [UC-14: Create friendly match](#uc-14-create-friendly-match)
* [UC-15: Navigate friendly matches](#uc-15-navigate-friendly-matches)
* [UC-16: Navigate current activity](#uc-16-navigate-current-activity)
* [UC-17: Join a public league](#uc-17-join-a-public-league)
* [UC-18: Join a private league](#uc-18-join-a-private-league)
* [UC-19: Join a public friendly match](#uc-19-join-a-public-friendly-match)
* [UC-20: Join a private friendly match](#uc-20-join-a-private-friendly-match)
* [UC-21: Configure team for upcoming match](#uc-21-configure-team-for-upcoming-match)
* [UC-22: Leave a league](#uc-22-leave-a-league)
* [UC-23: Cancel league](#uc-23-cancel-league)
* [UC-24: Leave a friendly match](#uc-24-leave-a-friendly-match)
* [UC-25: Cancel friendly match](#uc-25-cancel-friendly-match)
* [UC-26: Start a league](#uc-26-start-a-league)
* [UC-27: Start a friendly match](#uc-27-start-a-friendly-match)
* [UC-28: Leave the match view](#uc-28-leave-the-match-view)
* [UC-29: Navigate league](#uc-29-navigate-league)
* [UC-30: Spectate a match](#uc-30-spectate-a-match)
* [UC-31: “Re-enter” a match](#uc-31-re-enter-a-match)
* [UC-32: Change live behavior](#uc-32-change-live-behavior)
* [UC-33: Call for a substitution](#uc-33-call-for-a-substitution)
* [UC-34: Consult results of a match](#uc-34-consult-the-results-of-a-match)
* [UC-35: Navigate global ranking](#uc-35-navigate-global-ranking)

---

## UC-01 USER REGISTRATION

| UC-01 | USER REGISTRATION | |
| - | - | - |
| **Description** | Provides the mechanism for a new user to create an account within the system. | |
| **Actors** | USER | |
| **Preconditions** | The user is not currently registered and has navigated to the registration interface. | |
| **Postconditions** | A new user profile is persisted in the database with the provided credentials. | |
| **Main Success Scenario** | **\#** | **Action (Actor)** |
| | 1 | The user submits the required registration data: Name, Email, Password, Club Name, and Club Badge. |
| | 2 | The system validates the input, persists the new user record, and confirms successful registration. |
| **Exceptions** | \# | **Action (Actor)** |
| | 2.1 | In case required fields are missing, the system must display a validation error and prompts for completion. |
| | 2.2 | In case the email is already registered, the system must redirect the user to the login interface ([UC-02](#uc-02-user-login)). |

## UC-02 USER LOGIN

| UC-02 | USER LOGIN | |
| - | - | - |
| **Description** | The process by which an existing user authenticates to access protected system features. | |
| **Actors** | USER | |
| **Preconditions** | The user possesses a valid registered account ([UC-01](#uc-01-user-registration)). | |
| **Postconditions** | The user is authenticated and granted an active session within the application. | |
| **Main Success Scenario** | **\#** | **Action (Actor)** |
| | 1 | The user provides their registered Email and Password. |
| | 2 | The system verifies the credentials against the database. |
| | 3 | The system establishes a session and grants access to the user interface. |
| **Exceptions** | \# | **Action (Actor)** |
| | 2.1 | In case fields are empty, the system must notify the user and awaits valid input. |
| | 2.2 | In case the email does not exist, the system must return an authentication error. |
| | 2.3 | In case the password is incorrect, the system must return an "Invalid Credentials" message. |

## UC-03 USER LOGOUT

| UC-03 | USER LOGOUT | |
| - | - | - |
| **Description** | The process of terminating an active user session. | |
| **Actors** | USER | |
| **Preconditions** | The user has an established, authenticated session ([UC-02](#uc-02-user-login)). | |
| **Postconditions** | The session is invalidated, and the user is redirected to the login screen. | |
| **Main Success Scenario** | **\#** | **Action (Actor)** |
| | 1 | The user selects the logout option. |
| | 2 | The system destroys the session tokens and confirms the disconnection. |
| **Exceptions** | \# | **Action (Actor)** |
| | \- | None |

## UC-04 NAVIGATE PROFILE

| UC-04 | PROFILE | |
| - | - | - |
| **Description** | The user browses their profile. | |
| **Actors** | USER | |
| **Preconditions** | The user is authenticated.([UC-02](#uc-02-user-login)) | |
| **Postconditions** | The system successfully displays the profile interface. | |
| **Main Success Scenario** | **\#** | **Action (Actor)** |
| | 1 | The user selects the option to view their profile. |
| | 2 | The system displays the user profile, including badge and management options. |
| **Exceptions** | \# | **Action (Actor)** |
| | \- | None |

## UC-05 EDIT CLUB

| UC-05 | EDIT CLUB | |
| - | - | - |
| **Description** | The process where the user modifies their clubs name and badge | |
| **Actors** | USER | |
| **Preconditions** | The user is authenticated ([UC-02](#uc-02-user-login)). | |
| **Postconditions** | The modified club details are saved in the database. | |
| **Main Success Scenario** | **\#** | **Action (Actor)** |
| | 1 | The user modifies the desired fields of their club (name, badge) and submits the changes. |
| | 2 | The system validates the new data, updates the record, and confirms the successful modification. |
| **Exceptions** | \# | **Action (Actor)** |
| | 2.1 | In case no field has been modified, the system must display a validation error and prompts for completion. |

## UC-06 CREATE PLAYER

| UC-06 | CREATE PLAYER | |
| - | - | - |
| **Description** | The user chooses the stats and a unique name and number for a new player | |
| **Actors** | USER | |
| **Preconditions** | The user has an established, authenticated session ([UC-02](#uc-02-user-login)). | |
| **Postconditions** | The new player is saved into the database | |
| **Main Success Scenario** | **\#** | **Action (Actor)** |
| | 1 | The user selects the option to create a new player. |
| | 2 | The user inputs the required fields to create a player (name, number, stats) |
| | 3 | The system validates the input, persists the new player, and confirms successful registration. |
| **Exceptions** | \# | **Action (Actor)** |
| | 3.1 | In case required fields are missing, the system must display a validation error and prompts for completion. |
| | 3.2 | In case the name or number is already in use, the system must display a validation error and prompts for completion. |

## UC-07 DELETE PLAYER

| UC-07 | DELETE PLAYER | |
| - | - | - |
| **Description** | The user removes permanently a selected player from their squad. | |
| **Actors** | USER | |
| **Preconditions** | The user has at least one player created ([UC-06](#uc-06-create-player)) that is not assigned to the default team ([UC-11](#uc-11-create-default-team)). | |
| **Post-conditions** | The player is deleted from the database and removed from the user's squad. | |
| **Main Success Scenario** | **\#** | **Action (Actor)** |
| | 1 | The user selects an existing player to delete from their list. |
| | 2 | The system prompts the user with a confirmation dialog to prevent accidental deletion. |
| | 3 | The user confirms the deletion. |
| | 4 | The system deletes the player from the database and refreshes the list. |
| **Exceptions** | \# | **Action (Actor)** |
| | 2.1 | **I**n case the user cancels the confirmation dialog, the system must abort the deletion and return to the previous state. |

## UC-08 CREATE BEHAVIOR

| UC-08 | CREATE BEHAVIOR | |
| - | - | - |
| **Description** | The user creates a behavior | |
| **Actors** | USER | |
| **Preconditions** | The user is authenticated and has access to the behavior management interface. | |
| **Postconditions** | A new behavior is added to the user’s behavior list. | |
| **Main Success Scenario** | **\#** | **Action (Actor)** |
| | 1 | The user selects the option to create a new behavior. |
| | 2 | The user inputs the required fields to create a behavior (name, code) |
| | 3 | The system validates the input, persists the new behavior, and confirms successful registration. |
| **Exceptions** | \# | **Action (Actor)** |
| | 3.1 | In case required fields are missing, the system must display a validation error and prompts for completion. |
| | 3.2 | In case the name is already in use, the system must display a validation error and prompts for completion. |
| | 3.3 | In case the code is invalid, the system must display a validation error and prompts for correction. |

## UC-09 EDIT BEHAVIOR

| UC-09 | EDIT BEHAVIOR | |
| - | - | - |
| **Description** | The user edits a behavior. | |
| **Actors** | USER | |
| **Preconditions** | The user has at least one existing behavior created ([UC-08](#uc-08-create-behavior)). | |
| **Postconditions** | The behavior’s modified parameters are updated in the database. | |
| **Main Success Scenario** | **\#** | **Action (Actor)** |
| | 1 | The user selects an existing behavior to edit from their list. |
| | 2 | The user modifies the desired fields of the behavior (name, code) |
| | 3 | The system validates the new data, updates the record, and confirms the successful modification. |
| **Exceptions** | \# | **Action (Actor)** |
| | 3.1 | In case no field has been modified, the system must display a validation error and prompts for completion. |
| | 3.2 | In case the new name is already in use, the system must display a validation error and prompts for correction. |
| | 3.3 | In case the new code is invalid, the system must display a validation error and prompts for correction. |

## UC-10 DELETE BEHAVIOR

| UC-10 | DELETE BEHAVIOR | |
| - | - | - |
| **Description** | The user removes permanently a selected behavior from their list. | |
| **Actors** | USER | |
| **Preconditions** | The user has at least one existing behavior that is not associated with the default team (or is not in use). | |
| **Postconditions** | The selected behavior is permanently removed from the user’s behavior list. | |
| **Main Success Scenario** | **\#** | **Action (Actor)** |
| | 1 | The user selects an existing behavior to delete from their list. |
| | 2 | The system prompts the user with a confirmation dialog to prevent accidental deletion. |
| | 3 | The user confirms the deletion. |
| | 4 | The system deletes the behavior from the database and refreshes the list. |
| **Exceptions** | \# | **Action (Actor)** |
| | 2.1 | **I**n case the user cancels the confirmation dialog, the system must abort the deletion and return to the previous state. |

## UC-11 CREATE DEFAULT TEAM

| UC-11 | CREATE DEFAULT TEAM | |
| - | - | - |
| **Description** | The user configures a default starting lineup consisting of specific players, their assigned behaviors and a team formation for upcoming matches. | |
| **Actors** | USER | |
| **Preconditions** | The user has at least six players and one behavior in their list([UC-06](#uc-06-create-player) and [UC-08](#uc-08-create-behavior)). | |
| **Post-conditions** | A default team configuration is saved in the database and ready to be used in a league or friendly match. | |
| **Main Success Scenario** | **\#** | **Action (Actor)** |
| | 1 | The user navigates to the default team configuration screen. |
| | 2 | The user selects players from their squad to update a lineup. |
| | 3 | The user selects a behavior and assigns it to one or more players. |
| | 4 | The user selects a formation from the list. (1-1-1, 2-1, 1-2) |
| | 5 | The user confirms the selection. |
| | 6 | The system validates the data, updates the record, and confirms the successful modification. |
| **Exceptions** | \# | **Action (Actor)** |
| | 6.1 | In case not all the players have one associated behavior, the system must display a validation error and prompts for correction. |
| | 6.2 | In case the user has not selected a formation, the system must display a validation error and prompts for completion. |
| | 6.3 | In case the user selected less than six players, the system must display a validation error and prompts for completion. |

## UC-12 CREATE LEAGUE

| UC-12 | CREATE LEAGUE | |
| - | - | - |
| **Description** | The user establishes a new private or public league. | |
| **Actors** | USER | |
| **Preconditions** | The user has a default team ([UC-11](#uc-11-create-default-team)) | |
| **Post-conditions** | A new league will be created and will appear in the league list. | |
| **Main Success Scenario** | **\#** | **Action (Actor)** |
| | 1 | The user selects the option to create a new league.. |
| | 2 | The user inputs the required fields to create a league (name,max\_users,match\_time) |
| | 3 | The system validates the input, persists the new league, and confirms successful creation. |
| | 4 | The system displays the new league in the leagues’ list. |
| **Exceptions** | \# | **Action (Actor)** |
| | 3.1 | In case the user input enters the data in an incorrect format, the system must display a validation error and prompts for correction. |
| | 3.2 | In case required fields are missing, the system must display a validation error and prompts for completion. |
| | 3.3 | In case an input exceeds the bounds, the system must display a validation error and prompts for correction. |

## UC-13 NAVIGATE LEAGUES

| UC-13 | NAVIGATE LEAGUES | |
| - | - | - |
| **Description** | The user browses and lists the available leagues in the system. | |
| **Actors** | USER | |
| **Preconditions** | The user is authenticated and has access to the league list interface. | |
| **Post-conditions** | The system successfully displays a list of available leagues. | |
| **Main Success Scenario** | **\#** | **Action (Actor)** |
| | 1 | The user selects the option to list available leagues. |
| | 2 | The system displays a list of leagues that are available. |
| **Exceptions** | \# | **Action (Actor)** |
| | 2.1 | In case there are no leagues available, the system must display a message indicating the list is currently empty. |

## UC-14 CREATE FRIENDLY MATCH

| UC-14 | CREATE FRIENDLY MATCH | |
| - | - | - |
| **Description** | The user establishes a new private or public friendly match. | |
| **Actors** | USER | |
| **Preconditions** | The user has a default team ([UC-11](#uc-11-create-default-team)) | |
| **Post-conditions** | A new friendly match will be created and will appear in the friendly match list. | |
| **Main Success Scenario** | **\#** | **Action (Actor)** |
| | 1 | The user selects the option to create a new friendly match. |
| | 2 | The user inputs the required fields to create a match (match\_time) |
| | 3 | The system validates the input, persists the new friendly match, and confirms successful creation. |
| **Exceptions** | \# | **Action (Actor)** |
| | 3.1 | In case the user input enters the data in an incorrect format, the system must display a validation error and prompts for correction. |
| | 3.2 | In case required fields are missing, the system must display a validation error and prompts for completion. |
| | 3.3 | In case an input exceeds the bounds, the system must display a validation error and prompts for correction. |

## UC-15 NAVIGATE FRIENDLY MATCHES

| UC-15 | NAVIGATE FRIENDLY MATCHES | |
| - | - | - |
| **Description** | The user browses and lists the available friendly matches in the system. | |
| **Actors** | USER | |
| **Preconditions** | The user is authenticated and has access to the friendly match list interface. | |
| **Post-conditions** | The system successfully displays a list of available friendly matches.. | |
| **Main Success Scenario** | **\#** | **Action (Actor)** |
| | 1 | The user selects the option to list available friendly matches. |
| | 2 | The system displays a list of friendly matches that are available. |
| **Exceptions** | \# | **Action (Actor)** |
| | 2.1 | In case there are no friendly matches available, the system must display a message indicating the list is currently empty. |

## UC-16 NAVIGATE CURRENT ACTIVITY

| UC-16 | NAVIGATE CURRENT ACTIVITY | |
| - | - | - |
| **Description** | The user browses and lists their current match/league activity. | |
| **Actors** | USER | |
| **Preconditions** | The user is authenticated and has access to the current activity list interface. | |
| **Post-conditions** | The system successfully displays a list of the user’s current activity.. | |
| **Main Success Scenario** | **\#** | **Action (Actor)** |
| | 1 | The user selects the option to see current activity. |
| | 2 | The system displays a list of all current matches/leagues in which the user is involved. |
| **Exceptions** | \# | **Action (Actor)** |
| | 2.1 | In case there are no current matches or leagues, the system must display a message indicating the list is currently empty. |

## UC-17 JOIN A PUBLIC LEAGUE

| UC-17 | JOIN A PUBLIC LEAGUE | |
| - | - | - |
| **Description** | The user joins a public league. | |
| **Actors** | User | |
| **Preconditions** | The user has a default team ([UC-11](#uc-11-create-default-team)) and is navigating in the league list ([UC-13](#uc-13-navigate-leagues)). | |
| **Post-conditions** | The user’s club appears in the public league interface and is also displayed in the “current activity” section. | |
| **Main Success Scenario** | **\#** | **Action (Actor)** |
| | 1 | The user selects an available public league from the list. |
| | 2 | The user clicks the option to join the league. |
| | 3 | The system registers the user's club into the league and displays a confirmation message. |
| **Exceptions** | \# | **Action (Actor)** |
| | 3.1 | In case the league was started by the creator while the user was joining, the system must reject the registration. |
| | 3.2 | In case the league reaches its maximum capacity before the user joins, the system displays an error message. |

## UC-18 JOIN A PRIVATE LEAGUE

| UC-18 | JOIN A PRIVATE LEAGUE | |
| - | - | - |
| **Description** | The user joins a private league. | |
| **Actors** | User | |
| **Preconditions** | The user has a default team ([UC-11](#uc-11-create-default-team)) and is navigating in the league list ([UC-13](#uc-13-navigate-leagues)). | |
| **Post-conditions** | The user's club appears in the private league interface and is also displayed in the “current activity” section. | |
| **Main Success Scenario** | **\#** | **Action (Actor)** |
| | 1 | The user selects a private league and enters the league password. |
| | 2 | The system registers the user's club into the league and displays a confirmation message. |
| **Exceptions** | \# | **Action (Actor)** |
| | 1.1 | If the user enters incorrect data, the system will not grant access to the league and will prompt them to enter valid data. |
| | 1.2 | If data is missing, the system will not allow access to the league and will ask you to complete the missing information. |
| | 2.1 | In case the league reaches its maximum capacity before the user joins, the system displays an error message. |
| | 2.2 | In case the league was started by the creator while the user was joining, the system must reject the registration. |

## UC-19 JOIN A PUBLIC FRIENDLY MATCH

| UC-19 | JOIN A PUBLIC FRIENDLY MATCH | |
| - | - | - |
| **Description** | The user joins a public friendly match. | |
| **Actors** | User | |
| **Preconditions** | The user has a default team ([UC-11](#uc-11-create-default-team)) and is navigating in the friendly matches list ([UC-15](#uc-15-navigate-friendly-matches)). | |
| **Post-conditions** | The user’s club appears in the friendly match interface and is also displayed in the “current activity” section. | |
| **Main Success Scenario** | **\#** | **Action (Actor)** |
| | 1 | The user selects an available public friendly match from the list. |
| | 2 | The user clicks the option to join the friendly match. |
| | 3 | The system registers the user's club into the friendly match and displays a confirmation message. |
| **Exceptions** | \# | **Action (Actor)** |
| | 3.3 | In case the match was occupied while the user was joining, the system must reject the registration. |

## UC-20 JOIN A PRIVATE FRIENDLY MATCH

| UC-20 | JOIN A PRIVATE FRIENDLY MATCH | |
| - | - | - |
| **Description** | The user joins a private friendly match. | |
| **Actors** | User | |
| **Preconditions** | The user has a default team ([UC-11](#uc-11-create-default-team)) and is navigating in the friendly matches list ([UC-15](#uc-15-navigate-friendly-matches)). | |
| **Post-conditions** | The user's club appears in the private friendly match interface and is also displayed in the “current activity” section. | |
| **Main Success Scenario** | **\#** | **Action (Actor)** |
| | 1 | The user selects a private friendly match and enters the match password. |
| | 2 | The system registers the user's club into the match and displays a confirmation message. |
| **Exceptions** | \# | **Action (Actor)** |
| | 2.1 | If the user enters incorrect data, the system must not grant access to the match and must display a validation error and prompts for correction.. |
| | 2.2 | In case the match is occupied while the user is joining, the system must reject the registration. |
| | 2.3 | In case the match was occupied while the user was joining, the system must reject the registration. |

## UC-21 CONFIGURE TEAM FOR UPCOMING MATCH

| UC-21 | CONFIGURE TEAM FOR UPCOMING MATCH | |
| - | - | - |
| **Description** | The user edits their default team, associated behaviors and formation to join a league or to start a friendly match. | |
| **Actors** | USER | |
| **Preconditions** | The user has a default team configured ([UC-11](#uc-11-create-default-team)) and has entered a pre-match lobby. | |
| **Post-conditions** | The custom lineup for the specific match is saved. | |
| **Main Success Scenario** | **\#** | **Action (Actor)** |
| | 1 | The user accesses the pre-match formation interface. |
| | 2 | The user selects the starting players and custom behaviors for the match. |
| | 3 | The user selects a custom formation from the list. |
| | 4 | The user confirms the selection. |
| | 5 | The system validates the lineup and applies the formation to the upcoming match. |
| **Exceptions** | \# | **Action (Actor)** |
| | 5.1 | In case the pre-match countdown timer expires before the user confirms, the system automatically falls back to the user's default team ([UC-11](#uc-11-create-default-team)). |

## UC-22 LEAVE A LEAGUE

| UC-22 | LEAVE A LEAGUE | |
| - | - | - |
| **Description** | The user removes their club from a league that has not yet started. | |
| **Actors** | User | |
| **Preconditions** | The user joined a public or private league and it has not yet started. | |
| **Post-conditions** | The user's club is removed from the league roster. | |
| **Main Success Scenario** | **\#** | **Action (Actor)** |
| | 1 | The user selects the button to leave the league. |
| | 2 | The system displays a confirmation dialog box to prevent the user from accidentally leaving. |
| | 3 | The user confirms the exit. |
| | 4 | The system removes the club from the league participant list and updates the available slots. |
| **Exceptions** | \# | **Action (Actor)** |
| | 2.1 | In case the user cancels the confirmation dialog, the system must abort the operation. |
| | 4.1 | In case the league creator starts the league before the exit is processed, the system denies leaving and notifies the user that the tournament is active. |

## UC-23 CANCEL LEAGUE

| UC-23 | CANCEL LEAGUE | |
| - | - | - |
| **Description** | The user who created the league cancels it before it begins. | |
| **Actors** | USER | |
| **Preconditions** | The user created the league ([UC-12](#uc-12-create-league)) and it has not yet started. | |
| **Post-conditions** | The league is permanently deleted from the system and removed from the active leagues list. | |
| **Main Success Scenario** | **\#** | **Action (Actor)** |
| | 1 | The user navigates to the management panel of their created league and selects the option to cancel it. |
| | 2 | The system displays a confirmation dialog box to prevent the user from canceling by mistake. |
| | 3 | The user confirms the cancellation. |
| | 4 | The system deletes the league record, removes all registered participants, and confirms the dissolution to the user. |
| **Exceptions** | \# | **Action (Actor)** |
| | 3.1 | In case the user cancels the confirmation dialog, the system aborts the operation and returns to the league panel. |

## UC-24 LEAVE A FRIENDLY MATCH

| UC-24 | LEAVE A FRIENDLY MATCH | |
| - | - | - |
| **Description** | The user removes their club from a friendly match that has not yet started. | |
| **Actors** | User | |
| **Preconditions** | The user joined a public or private match and it has not yet started. | |
| **Post-conditions** | The user's club is removed from the match and the match re-appears in the “friendly match” list. | |
| **Main Success Scenario** | **\#** | **Action (Actor)** |
| | 1 | The user selects the button to leave the match. |
| | 2 | The system displays a confirmation dialog box to prevent the user from accidentally leaving. |
| | 3 | The user confirms the exit. |
| | 4 | The system removes the club from the match. |
| **Exceptions** | \# | **Action (Actor)** |
| | 2.1 | In case the user cancels the confirmation dialog, the system must abort the operation. |
| | 4.1 | In case the match creator starts the match before the exit is processed, the system denies leaving and notifies the user that the match is active. |

## UC-25 CANCEL FRIENDLY MATCH

| UC-25 | CANCEL FRIENDLY MATCH | |
| - | - | - |
| **Description** | The user who created the friendly match cancels it before it begins. | |
| **Actors** | USER | |
| **Preconditions** | The user created the friendly match ([UC-14](#uc-14-create-friendly-match)) and it has not yet started. | |
| **Post-conditions** | The match is permanently deleted from the system and removed from the active matches list. | |
| **Main Success Scenario** | **\#** | **Action (Actor)** |
| | 1 | The user navigates to the management panel of their created match and selects the option to cancel it. |
| | 2 | The system displays a confirmation dialog box to prevent the user from canceling by mistake. |
| | 3 | The user confirms the cancellation. |
| | 4 | The system deletes the match record, removes the opponent if they joined, and confirms the dissolution to the opponent. |
| **Exceptions** | \# | **Action (Actor)** |
| | 3.1 | In case the user cancels the confirmation dialog, the system aborts the operation and returns to the match panel. |

## UC-26 START A LEAGUE

| UC-26 | START A LEAGUE | |
| - | - | - |
| **Description** | The league creator starts the tournament, locking participants and generating the fixture. | |
| **Actors** | USER | |
| **Preconditions** | The user created the league([UC-12](#uc-12-create-league)), the league has not yet started and has the required number of participants. | |
| **Post-conditions** | The league starts, appears live in the “current activity” section and disappears from the list of available leagues. | |
| **Main Success Scenario** | **\#** | **Action (Actor)** |
| | 1 | The user navigates to their league management screen and selects the option to start the league. |
| | 2 | The system generates the fixtures for all registered clubs. |
| | 3 | The system updates the league status to “in progress”, closes new registrations and displays a successful notification. |
| **Exceptions** | \# | **Action (Actor)** |
| | 3.1 | In case one or more users leave the league before it has started (now the league is under the required number of players) the system must deny starting and notify the user that the league has not reached the required number of players. |

## UC-27 START A FRIENDLY MATCH

| UC-27 | START A FRIENDLY MATCH | |
| - | - | - |
| **Description** | The friendly match creator starts the match. | |
| **Actors** | USER | |
| **Preconditions** | The user created the friendly match([UC-14](#uc-14-create-friendly-match)), the match has not yet started and has an opponent. | |
| **Post-conditions** | The match starts,  appears live in the “current activity” list and disappears from the list of available matches. | |
| **Main Success Scenario** | **\#** | **Action (Actor)** |
| | 1 | The user navigates to their match management screen and selects the option to start the friendly match. |
| | 2 | The system updates the league status to “in progress”, and displays a successful notification. |
| **Exceptions** | \# | **Action (Actor)** |
| | 2.1 | In case the opponent leaves the match before it has started the system must deny starting and notify the user that the match has not reached the required number of players. |

## UC-28 LEAVE THE MATCH VIEW

| UC-28 | LEAVE A MATCH VIEW | |
| - | - | - |
| **Description** | The user intentionally exits an ongoing match (either as a playing manager or a spectator). | |
| **Actors** | USER | |
| **Preconditions** | The user is connected to a live match interface. | |
| **Post-conditions** | The user session is disconnected from the live match feed and redirected to the previous page. | |
| **Main Success Scenario** | **\#** | **Action (Actor)** |
| | 1 | The user selects the option to leave the live match. |
| | 2 | The system disconnects the user from the match stream, automatically replaces them with a bot (if they were actively playing), and redirects them to the Home view. |
| **Exceptions** | \# | **Action (Actor)** |

## UC-29 NAVIGATE LEAGUE

| UC-29 | NAVIGATE LEAGUE | |
| - | - | - |
| **Description** | The user browses an active league's dashboard to view group divisions, match fixtures, live scores, and current standings. | |
| **Actors** | USER | |
| **Preconditions** | The user is authenticated and is a participating member of the selected active league. | |
| **Post-conditions** | The system successfully displays the league's fixtures, groups, and standings to the user. | |
| **Main Success Scenario** | **\#** | **Action (Actor)** |
| | 1 | The user selects an active league from their current activity list. |
| | 2 | The system retrieves the league data from the database (group divisions, match schedules, live match statuses, and the points table). |
| | 3 | The system displays the league dashboard, presenting the fixtures grouped by stage with their respective states(incoming, active, finished) |
| | 4 | The system concurrently displays the updated standings table showing the position, club name, goals, and points. |
| **Exceptions** | \# | **Action (Actor)** |
| | 2.1 | In case the selected league has been cancelled or no longer exists, the system displays an error message and redirects the user to the home screen. |

## UC-30 SPECTATE A MATCH

| UC-30 | SPECTATE A MATCH | |
| - | - | - |
| **Description** | The user enters an active match as a spectator. | |
| **Actors** | USER | |
| **Preconditions** | The user is a member of the league. | |
| **Post-conditions** | The user connects to the live match simulation stream without player control privileges. | |
| **Main Success Scenario** | **\#** | **Action (Actor)** |
| | 1 | The user browses the active matches list and selects the "Watch Live" option for a specific match. |
| | 2 | The system verifies that the match is currently running. |
| | 3 | The system connects the user to the live match in spectator mode |
| **Exceptions** | \# | **Action (Actor)** |
| | 2.1 | In case the selected match ends right before the spectator successfully connects, the system redirects the user to the final match results screen. |

## UC-31 “RE-ENTER” A MATCH

| UC-31 | “RE-ENTER” A MATCH | |
| - | - | - |
| **Description** | The user "re-enters" a game they had previously left. | |
| **Actors** | User | |
| **Preconditions** | The match can't be over yet. and the user is in the current activity list. | |
| **Post-conditions** | The user joins the match that was in progress in real time. | |
| **Main Success Scenario** | **\#** | **Action (Actor)** |
| | 1 | The user selects the match in the "Home" section, from the current activity list. |
| | 2 | The system verifies the status of the match. |
| | 3 | The system redirects the user to the match. |
| **Exceptions** | \# | **Action (Actor)** |
| | \- | **Modified**:  was the response to a precondition. |

## UC-32 CHANGE LIVE BEHAVIOR

| UC-32 | CHANGE LIVE BEHAVIOR | |
| - | - | - |
| **Description** | The user changes the behavior of a first team player live during the match. | |
| **Actors** | User | |
| **Preconditions** | The user is in an active live match and has alternative behaviors saved on their profile. | |
| **Post-conditions** | The selected player’s behavior is updated and applied to the next calculation tick of the game. | |
| **Main Success Scenario** | **\#** | **Action (Actor)** |
| | 1 | The user selects a player currently on the field. |
| | 2 | The system displays a list of the user’s available behaviors. |
| | 3 | The user selects a new behavior and confirms the change. |
| | 4 | The system updates the player’s active behavior in the match in the next tick and confirms the change. |
| **Exceptions** | \# | **Action (Actor)** |
| | 3.1 | If the match ends exactly before the change is confirmed, the system aborts the operation and notifies the user. |

## UC-33 CALL FOR A SUBSTITUTION

| UC-33 | CALL FOR A SUBSTITUTION | |
| - | - | - |
| **Description** | The user requests a live substitution during the cooling break or the half time, involving any number of players from the bench. | |
| **Actors** | User | |
| **Preconditions** | The user is in an active match, during the stage of cooling break or halftime. The substitute player cannot have played on the field previously. | |
| **Post-conditions** | The system updates the team’s lineup for the remaining time of the game. | |
| **Main Success Scenario** | **\#** | **Action (Actor)** |
| | 1 | The user selects one or more players to substitute. |
| | 2 | The user selects the substitutes who will play. |
| | 3 | The user confirms the substitutions. |
| | 4 | The system validates the substitution rules(same amount of players and substitutes). |
| | 4 | The system adds the players selected for the bench to the team, and adds those selected for the field of play to the bench. |
| **Exceptions** | \# | **Action (Actor)** |
| | 3.1 | If the user cancels the substitutions, the system will abort the operation. |
| | 4.1 | If the number of players does not match the number of substitutes for the substitution, the system will prompt the user to select the correct number of players. |

## UC-34 CONSULT THE RESULTS OF A MATCH

| UC-34 | CONSULT THE RESULTS OF A MATCH | |
| - | - | - |
| **Description** | The user views a summary list of their previously played matches, including the outcome, match type, opponent, and date. | |
| **Actors** | User | |
| **Preconditions** | The user is authenticated and has completed at least one match. | |
| **Post-conditions** | The system successfully displays the play history summary list to the user. | |
| **Main Success Scenario** | **\#** | **Action (Actor)** |
| | 1 | The user selects the "Play history" option from their club profile menu. |
| | 2 | The system retrieves the user's match records from the database. |
| | 3 | The system displays the list of past matches, indicating for each one: the outcome (Victory/Defeat), match type (Friendly/League), opponent name, and date. |
| **Exceptions** | \# | **Action (Actor)** |
| | 2.1 | In case the user has no recorded matches yet, the system displays a message indicating that the play history is currently empty. |

## UC-35 NAVIGATE GLOBAL RANKING

| UC-35 | NAVIGATE GLOBAL RANKING | |
| - | - | - |
| **Description** | The user consults the global ranking. | |
| **Actors** | User | |
| **Preconditions** | The user is authenticated. | |
| **Post-conditions** | The system displays the global ranking leaderboard to the user. | |
| **Main Success Scenario** | **\#** | **Action (Actor)** |
| | 1 | The user selects the button to view the global ranking |
| | 2 | The system retrieves the global ranking data from the database. |
| | 3 | The system displays the sorted leaderboard, showing the ranked clubs and their points. |
| **Exceptions** | \# | **Action (Actor)** |
| | 2.1 | In case there are no players, the system must display a message indicating the list is currently empty. |
| | 2.2 | In case the global ranking data is temporarily unavailable or updating, the system displays an error message and aborts the operation. |
