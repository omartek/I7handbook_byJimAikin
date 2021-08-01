## The Names of Things {#the-names-of-things}

When creating objects, it’s a good idea to add an adjective to the name. When possible, the adjective should be unique, not a word that can also be used with other objects. This is not required, but failing to do it can get you into trouble. Here’s a simple example that shows why:

```inform7
The red potion vial is an open container on the table.
The red potion is in the red potion vial. [Error!]
```

This code won’t compile. The compiler complains, “You wrote 'The red potion is in the red potion vial': but this asks to put something inside itself, like saying 'the bottle is in the bottle'.” The compiler gets confused because all of the words that can refer to the red potion can also apply to the vial. The solution is simple: Just give the vial and potion their own names:

```inform7
The red vial is an open container on the table.
The healing potion is in the red vial.
```

In a real game, we’d need to write more code than this. For one thing, the way this has been written, the player could pick up the potion, which would be silly because the potion is probably be a liquid. Inform doesn’t know that a thing is a liquid unless you do some extra work. If you’re curious about liquid handling, you can consult page **10.2** of the _Recipe Book._ Liquids, ropes, and fire are among the more awkward concepts to implement in interactive fiction. For now, though, we’re just talking about giving things distinctive names.

Here’s a more complicated version of the same problem. Let’s suppose you’ve created three keys in your game — a rusty key, a silver key, and a third object called simply the key. Inform will let you do this, as long as you define the plain old key (not an object called “the plain old key” but the key with no adjectives) first in your source code. During the course of the game, the player might be carrying all three of the keys, and might need to unlock a door using the one that you’ve called simply “key”. This will cause a bug to appear in your game. The output will look like this:

```
>unlock door with key
Which key do you mean, the rusty key, the silver key, or the key?

>key
Which key do you mean, the rusty key, the silver key, or the key?
```

The question above goes by the fancy term _disambiguation_. The parser is attempting to figure out what the player’s input means. It comes up with two or more possible meanings, and has no way to decide which is correct, because the input is ambiguous — the parser doesn’t know which key object the player is referring to. The command UNLOCK DOOR WITH KEY could mean several different things, so the parser needs to ask the player to provide more information. The parser tries to get rid of the ambiguity by asking the player to add some detail.

As long as the player wants to use the silver key or the rusty key, this is not a problem: The parser’s question can be answered SILVER or RUSTY and the game will proceed as planned. But if the player needs to use the plain key, the one for which there’s no adjective, the player is stuck: There’s no way to tell the parser that you mean the plain old key, other than by going into a different room, entering the commands DROP SILVER KEY and DROP RUSTY KEY, and then returning to the room with the locked door. To avoid giving your players headaches, be sure to give each key its own adjective when naming it.

Inform is very unusual among programming languages, by the way, in allowing you to name objects using spaces between words. Most programming languages would require that the various key objects above be named silver_key and rusty_key (using the underscore character), silverKey and rustyKey, or with some other combination of letters. The text name (what the player reads while playing the game) would be a separate piece of data. But in Inform, when you call something the silver key in your source code, you’re creating both a code name (silver key) and a name for output text purposes (“silver key”). There are times when the two types of names need to be separate, and in Chapter 9, “Phrasing and Punctuation,” you’ll learn how to set that up (see [here](../chapter_9_phrasing_&_punctuation/the_names_of_things.md#the-names-of-things)).
