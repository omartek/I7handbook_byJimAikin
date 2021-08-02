#After
One of the rulebooks used in processing player commands.

#backdrop
 A special kind of object that can be in many rooms at once.

#Before
One of the rulebooks used in processing player commands.

#beta-testing
The second stage in testing a piece of software (such as a game) before it’s released. The first stage, alpha-testing, is typically carried out by the author or by the development team.

#brief mode
A mode of gameplay in which complete room descriptions are printed only the first time the player enters a room. Brief mode is the opposite of verbose mode.

#bug
An error in your code that causes it not to work the way you want it to, or not to compile at all.

#Carry Out
A set of rulebooks used in processing player commands. Each action has its own Carry Out rulebook.

#Check
A set of rulebooks used in processing player commands. Each action has its own Check rulebook.

#command prompt
The symbol that appears in the game at the beginning of the line where the player is supposed to type commands — usually the caret (>).

#comment
Material that’s in your source code but that is ignored by the compiler. In Inform, comments are surrounded with square brackets [like this].

#compiler
 The software “machine” within Inform that turns your source code into a playable game.

#container
A thing that the player can put other things into. Like a door, a container can be openable or lockable.

#default
A default is what Inform does automatically, unless you give it more specific instructions to do something different.

#device
A thing that can be switched on or switched off. (See p. 132.)

#door
A special kind of object that connects two rooms and that can be opened, closed, locked, and unlocked.

#extension
A file you can download that will add extra features to the Inform programming language. Extensions contain some Inform source code and also some documentation that tells you how to use the new features in the extension.

#Glulx
A game format suitable for large Inform games and those that include graphics and sound. Glulx games typically have filenames that end with .ulx or .blorb.

#holdall
A special type of portable container that the player can carry. If the player has a limited carrying capacity, an Inform game can automatically deposit excess objects in the holdall.

#IDE
Integrated Development Environment. The Inform 7 authoring system (which includes source code editing, built-in documentation, a compiler, an interpreter, an index of the compiled game, and so on) is an IDE.

#Index
A set of pages in the Inform program that give you quick access to just about everything in your game.

#Instead
One of the rulebooks used in processing player commands.

#interpreter
A piece of software that can run an interactive fiction game.

#kind
An abstract term used to create a class of similar things.

#noun
A special term that refers to whatever object the player mentioned first in the most recent command. For instance, if the player’s most recent command was PICK UP THE BALL, the value “the noun” will be set to the ball object.

#NPC
Non-player character — any of the other people (or, conceivably, talking animals) in a game other than the player character.

#parser
The software mechanism that reads the player’s input during a game and figures out what the input means. (See p. 26.).

#PC
The player character in a game, typically referred to in the game’s output text as “you.”

#printed name
The name Inform will use in the game when it needs to refer to the object. Usually, the printed name is whatever you called the object when creating it, but the printed name can be changed.

#property
A piece of data (such as text or a numeric value) that is attached to an object. Each object can have its own set of properties, and each property will be set to some particular value, either when the object is created or during the course of the story. Typically, kinds of object share many common properties.

#Recipe Book
The second book of Documentation in the Inform program.

#region
A related group of rooms within your model world. (See p. 78.)

#Report
A set of rulebooks used in processing player commands. Each action has its own Report rulebook. (See p. 148.)

#room
A location (either indoors or outdoors) in which some part of the game takes place.

#rule
An instruction that tells Inform what to do in a certain situation. Rules are gathered together by the compiler into rulebooks.

#scene
A portion of your game that is structured so as to happen during a certain period of time.

#scenery
A property that can be applied to things (including doors, supporters, and so on). When a thing is scenery, it will not be mentioned automatically in the game when the room description is printed; your room description will need to supply all mentions of scenery, so that the player will know the scenery object exists. Scenery can’t be picked up and carried around by the player.

#scope
The portion of the model world that is currently available to the player. Usually the scope is the same as the room the player is in, but in some special situations it may be different.

#second noun
A term that refers to the second object the player mentioned in a two-object command. For instance, if the player’s most recent command was PUT THE BALL IN THE BOX, the value “the second noun” would refer to the box object.

#Skein
A panel in the Inform 7 IDE that keeps track of and can replay all of your testing sessions with your project (or at least a large number of recent sessions).

#source code
Also called source text — what you write in the Source panel of Inform’s IDE.

#status line
The strip across the top of the window in a running game. Various types of information, such as the room name, score, and time of day within the game, can be displayed in the status line. (See p. 220.)

#supporter
A kind of object in an Inform game. A supporter is an object like a table, that other objects in the game can be placed _on_.

#switch
A group of lines of code. Inform will choose one line from the group depending on the current value of some variable.

#table
A data structure in which Inform can store related data in rows and columns. (See p. 268.)

#thing
The basic kind of object in an Inform game. Doors, supporters, containers, and even people are all things, but the term “thing” is sometimes used to refer specifically to movable objects that aren’t of any other kind.

#truth state
A kind of variable that can have only one of two values — true or false. (See p. 249.)

#variable
A value that changes while the game is running. A variable can be a number or an object, for example.

#verbose mode
A mode of gameplay in which complete room descriptions are printed each time the player enters a room. Verbose mode is the opposite of brief mode.

#virtual machine
A piece of software that creates a sort of “box” inside which other software (such as an Inform game) can run. It’s called a “virtual” machine because it isn’t an actual hardware machine.

#visible thing
An object that is somewhere in the model world of the game, but not necessarily visible to the player at this moment.

#wearable
A property of things. Wearable things can be worn by the player, or by other characters.

#Z-code
A type of compiled game that is compatible with the Z-machine. Inform can produce Z-code games in the .z8 format.

#Z-machine
An interpreter that can run games written in Inform. (Large games and games with special features such as graphics are written using Inform’s Glulx format, which is not compatible with the Z-machine.) Z-machine interpreters are available for most computer platforms, including many obsolete operating systems and some portable devices.
