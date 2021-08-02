## What Happens in a Game

If you’ve played a few parser-based interactive fiction games, you won’t need to be told how IF works. But for the benefit of those who may just be getting started, we’ll cover the basics here. Parser-based IF is a bit different from hypertext stories in which you move through the story by clicking or tapping links; we’ll have little more to say in the _Handbook_ about this type of user interface, though in fact some extensions to Inform (notably Keyword Interface by Aaron Reed) have been created that add the ability to insert clickable links in your story.

In a game, you play the part of a character in a story. The story may have a simple concept, or it may be quite complex, involving many characters, locations, and events. In a simple story, you (the character) might be wandering around in a cave, collecting treasures. In a complex story, you’ll most likely meet other characters, and you may need to outwit them or make friends with them. The story may have several different endings, some of them happy and others not so happy. One of your tasks as a player/reader will be to figure out which actions lead to a happy ending. But until you start taking actions, you won’t know which choices lead to which endings.

### Entering Commands

To play the game, you type _commands_ (instructions to the computer) when you see the command prompt. The command prompt generally looks like this:

&gt;

The words you type at the prompt are called the command line, and this method of interacting with the computer is called a _command line interface_ (CLI). The command line interface was common in computers in the 1970s, when interactive fiction was first invented, but today most computer users may not even know that their computer’s operating system has this type of interface. It’s well hidden.

Unlike a video game, where you need quick reflexes to deal with animated characters who are moving around, in a text game nothing happens until you type a command and hit the computer’s Enter key. When you press Enter, the game reads your latest command and prints out a response. (There are rare exceptions to this — text games that have some real-time features, which cause time to advance in the story whether or not you enter a command.)

What kinds of commands can you enter? The commands tend to have a common form, which we’ll discuss here, but each game may have a few unexpected commands of its own. Part of the challenge of interactive fiction (indeed, most of the challenge) is figuring out which commands to enter, and when. A command that works beautifully in one scene may not produce useful results in another. It’s up to the player to discover how exactly to use the commands in any given game.

Some of the responses that the game gives when you enter commands may be error messages: Maybe you misspelled a word, for instance, so the game doesn’t know what you meant. In this case, try typing OOPS followed by the correct spelling. The result might look like this:

```
Dungeon

A dank and dismal dungeon. You can go north.

You can see a tool chest (closed) here.

> open chet

You can't see any such thing.

> oops chest

It's awkward, but you manage to open the tool chest while wearing the handcuffs.
```

Assuming your command makes sense, the response will show you what’s happening in the story. The command you entered may cause a change in the world of the story, or it may just give you more details about what’s going on.

If you’re playing a game, you don’t often need to pause to think about exactly how the game is able to read your commands and respond to them. But while writing a game, you’ll need to know more than a few details. The software gadget that reads and interprets what the player types is called a **parser**. Every text game that uses a command line interface has a parser (although the parser used in games that are written using the ADRIFT programming system is so crude as almost not to be worthy of the name). The parser that’s built into Inform 7 is very sophisticated. It’s able to understand quite a variety of inputs from the player. You can also change what it does, if you need to. Many of the techniques for doing that are explained in this _Handbook._ For instance, you can add to the types of commands that the parser understands. You can also change the error messages that it prints out when it doesn’t understand what the player typed or can’t do the operation that the player has requested.

No parser is able to understand the kinds of complex sentences that you and I speak and write every day. The parser is designed to process simple commands, such as OPEN THE DOOR and PICK UP THE BALL. Most commands are of the form ```<VERB> <NOUN> <MAYBE A PREPOSITION> <MAYBE ANOTHER NOUN>```.

Some verbs (such as WAIT, SLEEP, and JUMP) are followed by no nouns at all. Some verbs need one noun — for instance, OPEN THE DOOR and PICK UP THE BALL. A few verbs take two nouns, which are (usually) separated by a preposition. Examples would include PUT THE BOX ON THE TABLE and HIT THE OGRE WITH THE STICK.

When you’re entering commands during a game, the word THE can always be left out, and most experienced players never use it. They would just type HIT OGRE WITH STICK. That works perfectly. (Or at least, it works perfectly if the player character is holding a stick, if there’s an ogre in the room, and if the author has taken the trouble to tell Inform what should happen in response to that command.) Think of the command line syntax in interactive fiction as a form of Caveman English. TAKE BALL. OPEN DOOR. It’s easy, once you get used to it.

If an object has a name that includes an adjective or two, you’ll probably be able to use just an adjective to refer to it. If the object is called “the tarnished gold crown” in the game, typing PICK UP GOLD should work (at least, it will work if the author has done a decent job writing the game).

>**It’s All About You!**
>
>In most interactive fiction, you (the player) play the part of a character called “you.” When the game prints out a message, such as “You can’t see any such thing,” it’s talking about the character called “you.” The pronoun “you” is grammatically in the second person, so we say these games are written in _second person_. A few games are written in which the character is “I” (first person) or “he” or “she” (third person).
>
>In most games, the action is described as taking place right now. For instance, “You walk up the stairs.” Grammatically, this is called _present tense._ A few games are written in past tense (“You walked up the stairs.”) Second-person, present-tense storytelling is not used much in novels or short stories, but it’s very normal in interactive fiction. It’s possible to write a story in any combination of person and tense, and the current version of Inform supports this very nicely. You might want to give a period flavor to a story set in the 18th century, for instance, by choosing past tense and third person: “He walked up the stairs.” For more on how to do this, see [here](../chapter_10_advanced_topics/story_tense_and_viewpoint.md/#story-tense-and-viewpoint).

Once in a while, the parser will ask the player for more information. For instance, if you’re in a room with a gold crown, a gold ring, and a gold orb, when you type PICK UP GOLD the parser will respond, “Which do you mean, the gold crown, the gold ring, or the gold orb?” At this point, the parser will try to interpret your next input as an answer to the question. If you just type ORB, the parser will understand that you meant PICK UP GOLD ORB, and the game will proceed to do that action.

If you’re in a room with another character, you can try giving them a command, like this: BOB, PICK UP THE STICK. Bob may or may not do what you want — at the moment, we’re just looking how commands are entered. Here, you type the name of the character, then a comma, then the command. (To learn how to write a game so that characters will respond to the player’s commands, see [here](../chapter_5_creating_characters/giving_orders_to_characters.md#giving-orders-to-characters).)

Most interactive stories take place in what’s called a _model world_. This is a place that was created by the author of the story. It exists only within the computer — and in fact, only within the game’s interpreter software. It might be an ancient castle, the interior of a space station, or a busy modern city. The model world always consists of one or more _rooms._ The rooms are the locations where the story takes place. A “room” might be a large open field, or it might be the interior of a small, stuffy cardboard box. The word “room” is used in IF authoring to refer to each of the locations in the game, whether or not the location is literally a room.

If you want to see what’s in the room with you, you can use the command LOOK (this can be abbreviated L). When you LOOK, you’ll read a description of the room and its contents. In general, you can only see what’s in the room with you; you can’t see into any other rooms. Some games have windows you can look through, but basically windows have to be “faked” using some clever programming tricks.

If there’s more than one room in the game, you’ll be able to move from room to room. This is usually done by typing commands based on compass directions — for instance, GO NORTH. This type of command is so common that it can be abbreviated. You can type N to go north, NE to go northeast, E to go east, SE to go southeast, and so on. Depending on the type of world where the story takes place, the directions you can travel may also include up (U), down (D), in, and out.

The use of compass directions in IF is artificial but convenient. From time to time authors try to come up with alternatives, but none of these has caught on. In “Blue Lacuna” (a large, complex game written in Inform), Aaron Reed used a neat system in which certain words that are highlighted in the text can be used as movement commands. For example, if the word “beach” appears highlighted, typing BEACH will take you to the beach. This system is available as an extension for Inform called Keyword Interface. (For more on how to use extensions, see [here](./extensions_for_inform.md#extensions_for_inform).)

As you travel through the model world, you’ll encounter various kinds of objects. Some of them will be portable: You’ll be able to pick them up, carry them around, and drop them in other locations. Other objects will be scenery, and can’t be moved.

The first thing you’ll want to do, when you enter a room, is EXAMINE all of the objects that are mentioned in the room description. Most modern games understand X as an abbreviation for EXAMINE, though a few old-school games don’t. Read the room description carefully and then X anything that’s mentioned. You may discover important details by doing this.

If an object is portable, you’ll be able to pick it up. Let’s say the object is a bowling ball. The commands PICK UP BALL, TAKE BALL, and GET BALL all mean the same thing. (Inform authors call this the _taking_ action.) To read a list of the items you’re carrying, use the INVENTORY command. This can be abbreviated INV, or simply I.

The game may limit, realistically, the number of objects you can carry at any given time — after all, the player character probably has only two hands! But players tend to find this limitation annoying. A compromise solution adopted by many authors is to give the player a sack, or something similar, whose capacity is basically unlimited. (To learn how to make a carry-all object for the player, see the “Inventory” section [here](../chapter_3_things/inventory.md#inventory).)

Whether or not a game contains a carry-all, from time to time you’ll probably find other containers. A container may be permanently open, like a basket, or it may be something that you can OPEN and CLOSE, like a suitcase. If a container is open, you can try putting things into it using a command like PUT BOWLING BALL IN THIMBLE. Some of the things that can be opened and closed can also be locked and unlocked.

Note that Inform’s standard locking and unlocking actions require that the author create a key that fits the lock. By default, the action UNLOCK DOOR is not defined in Inform, though you can create this type of action yourself, for your own game. Inform’s unlocking action always takes the form UNLOCK DOOR WITH RUSTY KEY. And of course the player must be holding the correct key for that action to work.

Most games include puzzles. (For more on puzzles, see Chapter 6.) Some puzzles are easy, and some are fiendishly difficult. These days, many games have built-in hints that will help you if you don’t know how to solve a puzzle, but in other games, it’s strictly up to your ingenuity to figure out what to do. To learn how to add hints to an Inform game, see [here](../chapter_10_advanced_topics/adding_hints.md#adding_hints).

Some games are friendly: You may get stuck for a while before you figure out what you need to do next, but the worst thing that can happen to the character whose role you’re playing is wandering around and not knowing what to do next. Other games are cruel. In a cruel game, if you do the wrong thing, your character can get killed, perhaps in a very nasty way. Fortunately, the UNDO command will usually get you out of trouble.

Not always, though. Some games are so cruel that they won’t let you UNDO if your character has died. Because of that, it’s a good idea to SAVE your game every so often, especially before trying anything that might be dangerous. If you get killed or lose the game in some other way, you’ll be able to RESTORE. The RESTORE command opens a dialog box where you can choose a saved file to reopen. By choosing the most recent saved file, you can revert to a point before you got in trouble. (Wouldn’t it be nice if real life was like that?)
