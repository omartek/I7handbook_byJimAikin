## Creating Your First Room {#creating-your-first-room}

Every Inform game has to have at least one room. Creating a room is easy; you do it like this:

```inform7
The Forest Path is a room.
```

![](../assets/graphics24.jpg)

This simple sentence produces an entire Inform game (though not a very interesting one). If you create a new game, type this sentence into the Source, and compile the game by clicking the Go button, you’ll find yourself in a (featureless) room called Forest Path.

It’s usually a good idea to capitalize the words in each room name. This is not required, it’s just a good habit to get into because it will produce a more professional-looking game. You can add “The” before the room name if you like. Inform will normally strip out the “The” before printing the room name in the game’s output, so a room you call The Forest Path will appear in the game as Forest Path. You can override this if you want to, though, using the **printed name** property, like this:

```inform7
The printed name of the Forest Path is “The Forest Path”.
```

Notice the punctuation in that sentence: The period is _outside_ the quotation mark, not inside. This is important. When Inform sees a period just before a close-quote, it will usually add an extra blank line in the game’s output each time it prints the text. This won’t happen when a room name is displayed — but even so, having room names that end with periods would be rather ugly. With a room name, putting the period outside the close-quote is the right thing to do.

You’ll almost always want to give each room its own **description**, to give the player some idea where she is. The description is text to be printed out, so you write it in double-quotes, like this, putting the description immediately after the sentence in which we created the room:

```inform7
Forest Path is a room. “Tall old trees surround you.”
```

The first sentence creates a room called Forest Path. The second sentence, in quotes, is the description of the room. If you put the description immediately after the sentence that creates the room, Inform will know that it’s the description; you don’t need to do anything specific to tell Inform that the second sentence is the room description. (This bit of streamlined coding does _not_ apply to other objects, as you’ll learn in the next chapter.)

If you’ve put something else between the sentence that creates the room and the description, however, you need to tell Inform what you’re doing. This won’t work:

```inform7
Forest Path is a room. The printed name of Forest Path is "The Forest Path." "Tall old trees surround you."
```

Instead, you need to do it this way:

```inform7
Forest Path is a room. The printed name of Forest Path is "The Forest Path." The description is "Tall old trees surround you."
```

A room description can be as long or short as you like. It always has to end with a period (or with a question mark or exclamation point, though those aren’t used much in room descriptions.) In this case we want the period _inside_ the quotation mark, because we want Inform to put a blank line after the description and before whatever is printed next.

> **Important: A Description Is Not a Description!**
>
>Just to make matters a little more confusing, Inform’s Documentation uses the word “description” in two entirely different ways. What we’re talking about in this chapter is the description _property_ of an object in the world of the story. This type of description is the text that will be printed out in the game when the object is examined (or when the room is examined using the LOOK command). However, Chapter 6 of _Writing with Inform_, “Descriptions,” uses the word in another sense — to refer to certain phrases you’ll use in your code — for instance, the text with which you specify the type of object you want to create. The phrase “openable container” is a description you would use in your code to specify that an object called cardboard box is something that the player will be able to open, close, and put things in. But this type of description is _not_ what the player will see on examining the cardboard box.

In describing the room, you’ll almost always find yourself mentioning things that can be seen in the room. They may be important to the story, or they may be there simply to add color and atmosphere. The things that are mentioned in the room description are _scenery_.

> **How Not to Describe a Room**
>
> When writing room descriptions, there are two traps to watch out for. First, try to avoid starting every room description with “You are in...” or “You are standing in....” This gets boring very quickly. Just describe the setting. Second, avoid describing the room as if the player has just arrived from any particular direction, or is facing any particular direction. As you’re first writing the game, you may naturally tend to assume that the player has arrived in the dining room from the front hall — but later in the game, the player may arrive in the dining room by returning from the kitchen. A good room description will give the same impression no matter where the player arrived from.

In general, it’s a very good idea to add a separate scenery object (see the next section) for each thing that’s mentioned in a room description. The people who play your game don’t start out knowing what’s important in the story and what’s irrelevant, so players usually run around examining any object that’s mentioned in the game’s output — or trying to examine it. If the player tries to examine something that isn’t in scope, the parser will respond, “You can’t see any such thing.” If the thing has just been mentioned in the room description, this message is annoying, and your players will soon decide you’re not trying very hard. Imagine this situation in a game:

```
Forest Path
Tall old trees surround you.

>x trees
You can’t see any such thing.
```

In the early days of interactive fiction, this type of response was considered normal, but at that time computers had much less memory. Game authors had to make the most of a tiny amount of text and a very small number of objects, so none could be wasted on irrelevant scenery. Today, failing to put the scenery into your rooms is considered poor form. In the next section of this chapter, we’ll look at how to add scenery.

It’s important to write room descriptions that give players a clear idea which directions are available for travel. That is, if the player can travel east, northeast, or west to reach other rooms, the room description should mention these directions and perhaps give some vague idea what lies in that direction:

```
Forest Path
Tall old trees surround you. The path runs roughly north and south from here, and a little side path runs off through the bushes to the northeast.
```

Failing to mention exits in the room description was used as a puzzle in some early games, but today this type of thing is generally considered rude and crude. Fortunately, there are extensions (such as Exit Lister by Eric Eve) that will put the room’s exits into the status line at the top of the game window. Using Exit Lister or something similar is a nice courtesy — but I feel it’s still a good idea to write a room description that describes all of the exits in a clear way (unless one of them is hidden as a puzzle). Exit Lister also provides a utility command for the player, EXITS, which will list the available exits to refresh the player’s memory.

Inform’s routines for printing out room descriptions are actually quite complex. After printing out the description you write, Inform will automatically mention anything in the room that it considers interesting — mainly people and visible objects (but not scenery; Inform assumes that the scenery needn’t be mentioned separately, presumably because you’ve already mentioned it in the room description). If you’ve added an object called a large toad to the room, Inform will know to mention it like this:

```
The Forest Path
Tall old trees surround you.

You can see a large toad here.
```

Inform uses certain rules for deciding how (or whether) to mention these things. If you want to customize the way room descriptions are printed out, see “Room Descriptions” at the end of this chapter.
