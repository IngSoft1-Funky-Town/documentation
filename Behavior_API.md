# Ingeniería del Software I

## Behaviors API

### Index

* [Data types](#data-types)
* [Environmental Variables](#environmental-variables)
* [Primitives for behaviors](#primitives-for-behaviors)
* [Functions and methods](#functions-and-methods)

---

## Data types

| Data type name | Description |
| - | - |
| coords | "coords" will be a synonim for a tuple with two integers (like a struct in C/C++). |
| percentage | "percentage" will be a synonim for an integer where the value can only be between 1 and 100. |

## Environmental Variables

| Variable Name | Data type | Description |
| - | - | - |
| posMe | *coords* | Returns position of the player |
| posBall | *coords* | Returns position of the ball |
| posOwnGoal | *coords* | Returns position of the user's goal |
| posRivalGoal | *coords* | Returns position of the user's opponent's goal |
| posTeammates | *array[(coords), (coords)]* | Returns an array with positions of the teammates |
| posRivals | *array[(coords), (coords), (coords)]* | Returns an array with positions of the opponent's players |
| goalsScored | *int* | Amount of goals scored |
| goalsReceived | *int* | Amount of goals received |
| canReachBall | *bool* | Is the player in **control** (attribute) to kick the ball? |
| ballInMyHalf | *bool* | Is the ball in my half of the field? |

## Primitives for behaviors

| Function Name | Function description |
| - | - |
| kickBall(coords: *coords*, powerPercentage: *percentage*) | Kick the ball to **coords** with **powerPercentage**% of his max power. |
| moveTo(coords: *coords*, speedPercentage: *percentage*) | Move to **coords** at **speedPercentage**% of his max speed. |

## Functions and methods

| Function Name | Returned value | Function description |
| - | - | - |
| distance(coord1: *coords*, coord2: *coords*) | *float* | Get the distance between two coordinates, **coord1** and **coord2**. |
| closest(reference: *coord*, compare: *list\[coords\]*) | *coords* | Get the closest position to **reference** in a **list of coordinates** |
