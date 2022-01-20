# Dungeon

This project implements a Dungeon game which consists of a grid of caves and tunnels through
which the player moves in order to reach the end location. The player is free to move in any
of the available directions and can pick treasure if he/she wants to. The player has the abilities
to move, pick arrows and treasures and shooting arrows. The game has a number of monsters, each
located in a cave that has the ability to kill the player in one shot. On the other hand, its takes
two shots of an arrow to kill the monster. The player can be located at a distance and shoot an
arrow in order to hit the monster.

This is a GUI as well as text-based implementation of this game where the user interacts with the
game via GUI or command-line. 

## Features

1. Generates a random maze everytime
2. Configurable grid size
3. Allows adding extra paths to the generated MST
4. Player can move freely
5. Player can pick treasure if he/she wants to
6. Monsters at different locations to hinder the player's goal
7. Weapons for the player to kill monsters
8. GUI as well as text-based mode

## How to execute

### To run as a GUI application
1. To execute the `Dungeon.jar`, make sure that _Java 11_ is installed on your system.
2. Open a Terminal(macOS) or CommandPrompt(Windows) and execute the following command to execute this game in GUI-mode:
   ```shell
   > java -jar /path/to/project/res/Dungeon.jar
   ```
   **Note:** Replace `/path/to/project/` as per your system.
3. The game should start based on the given configurations
4. To restart the same game, click on `Game > Restart Game`
5. To start a new game, click on `Game > New Game`
6. To quit, click on `Game > Quit`

### To run as a CLI application
1. To execute the `Dungeon.jar`, make sure that _Java 11_ is installed on your system.
2. Open a Terminal(macOS) or CommandPrompt(Windows) and execute the following command to execute this game in text-mode:
   ```shell
   > java -jar /path/to/project/res/Dungeon.jar [rows] [cols] [interconnectivity] [isWrapping] [treasureFreq] [monsterCount]
   ```
   **Note:** Replace `/path/to/project/` as per your system.
   **Note:** Replace `[rows] [cols] [interconnectivity] [isWrapping] [treasureFreq] [monsterCount]` as required by the program.
   1. Provide an integer value for `[rows]`
   2. Provide an integer value for `[cols]`
   3. Provide an integer value for `[interconnectivity]`
   4. Provide `true` or `false` for `[isWrapping]`
   5. Provide a floating value between 0.0 to 1.0 for `[treasureFreq]`
   6. Provide an integer value for `[monsterCount]`
3. The game should start based on the given configurations

## How to Use

### GUI mode
1. Press any of the arrow keys to move in that direction
2. Press `r` to pick all the available rubies from the current location
3. Press `d` to pick all the available diamonds from the current location
4. Press `s` to pick all the available sapphires from the current location
5. Press `a` to pick all the available arrows from the current location
6. Press ` `(space) along with any of the arrow keys to shoot an arrow in the given direction
7. Left-click on the neighbouring locations using mouse to move the player to that location

### Text mode
1. Enter move (or m) or pick (or p) or shoot (or s) to select a player action.
2. Enter NORTH or SOUTH or WEST or EAST when asked for next move.
3. Enter arrow or ruby or diamond or sapphire when asked for the item to be picked.
4. Enter a number between 1 - 5 and a direction (NORTH, SOUTH, EAST, WEST) to shoot the arrow.

## Description of the example

### GUI-mode example
1. The `res/GUI-sample.png` image shows the actual game screen that is divided into two parts:
   1. The left part shows the dungeon with only the explored locations, player's current location and details about different locations
   2. The right part has 2 components:
      1. The `Player Stats` component shows all the details about the player
      2. The `Things you can collect` component shows all the details about the current location
2. The `res/Help Menu.png` image shows the help modal which lists the key bindings for the game
3. The `res/New Game Modal.png` image shows the modal which allows the user to enter config details for the new game

### Text-mode example

All the runs has the following sections in the output:

1. For each move until the game is over:
   1. Show current game state
      1. Location type
      2. Treasures that can be picked
      3. Arrows that can be picked
      4. Smell information
      5. Player's health, arrows and treasures information
   2. Ask for the next action
      1. Ask for the input based on the selected action
2. Show game over

### Run 1 - res/run-1.txt
In this run, a non-wrapping 4x6 dungeon is created with 1 interconnectivity, 3 monsters and 20% 
treasure frequency. It shows that the player picks treasures, arrows, shoots the arrows, kills 
a monster and wins the game.

### Run 2 - res/run-2.txt
In this run, a wrapping 4x6 dungeon is created with 1 interconnectivity, 3 monsters and 20%
treasure frequency. It shows that the player is killed by the monster.

## Design Changes

### Project 5 changes

- Added ReadonlyDungeonGame interface that is extended by DungeonGame interface
- Added functionality to store and retrieve visited locations
- Added functionality to reset the game
- Added functionality to start a new game with different parameters
- Added a GUI which is implemented using Swing

### Project 4 changes

- Moved all the model code to `dungeon.model` package 
- Added Monster and MonsterInternal interfaces
- Added AbstractMonster and Otyugh classes
- Added monster related fields and methods to the LocationImpl and DungeonGameBuilder class
- Added SmellLevel enum
- Moved start and end locations to `DungeonImpl`
- Added arrow functionality to Player, Location and Dungeon
- Implemented the text-based controller

### Project 3 changes

- Renamed Game class to DungeonGame
- Renamed Player concrete class to PlayerImpl
- Made Dungeon class constructor package-private
- Changed the type of treasureCollected to List in PlayerImpl class
- Added a copy constructor to Location class
- Changed access modifier of releaseTreasure() and addTreasure() in Location to package-private
- Changed the datatype of Location id to integer
- Renamed GameBuilder class to DungeonGameBuilder
- Removed `generateLocations` method from MazeBuilder
- Added new methods and variables to MazeBuilder class
- Added Edge class
- Removed treasureKeeper variable from Dungeon
- Using Maps to implement treasure in Location and PlayerImpl class
- Added getAllCaves method to Dungeon class
- Renamed getStartEndLocation to getLocationPair class.
- Added PlayerInternal interface.
- Added copy constructors for Player and Dungeon classes
- Added getLocationAdjacencyList method in Dungeon class
- Renamed Location class to LocationImpl
- Added Location interface
- Renamed Dungeon class to DungeonImpl
- Added Dungeon and DungeonInternal interfaces
- Renamed DungeonGame to DungeonGameImpl
- Added DungeonGame interface

## Assumptions

- A cave can have multiple types of treasure and many counts of each type.
- Player does not always pick the treasure
- If interconnectivity is greater than the no. of possible edges, the whole maze will be interconnected.
- A cave can have at most one monster.
- If monster count is more than the available caves, then each cave will have one monster in it.
- A player wins if it reaches the end location that has an injured monster and if the player gets a chance to escape.

## Limitations

1. The player won't be able to pick the treasures from the end cave as the game is finished at the point.
2. Player must pick all the arrows in a location at once.
3. Player must pick all the treasure of same type at once.
4. Adding a new weapon is not easily achievable.
5. The game does not force the player to give escape direction if the player enters a cave with an injured monster and gets a chance to escape.

## Citations

Did not use any external sources for this project.