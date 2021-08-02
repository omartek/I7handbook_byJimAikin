## Adding More Rooms to the Map

![](../assets/graphics34.jpg)

It’s possible to write a complete short game that takes place in a single room. But most games will need a number of rooms. The player travels from one room to another using standard compass directions — NORTH (or simply N), SOUTHWEST (SW), and so on.

Other methods of travel have been tried by various authors, and you may want to experiment with them at some point. In “Blue Lacuna,” by Aaron Reed, you can travel from place to place by typing the name of something that lies in the direction that you want to go. In a game designed like this, CASTLE will take you closer to the castle (or cause you to enter it, if you’re already close), and so on. Aaron has released this system as an extension called Keyword Interface — but at this writing Keyword Interface is not yet fully compatible with 6L38\. (I’ve notified Aaron of the problem.) Even after it is upgraded, you’ll find that it’s more complex than the average extension, so you should expect to do some study and some testing in order to get it to work the way you’d like it to in your game.

If your story is set aboard a ship, you may want to replace N, S, E, and W with FORWARD, AFT, PORT, and STARBOARD. (**Example 42** in the Documentation, “Fore,” shows how to do this. **Page 3.26**, “Directions,” offers some other suggestions.) But for your first game, I’d suggest sticking with compass directions. All players who are not complete newcomers to IF will know how to use them.

Inform makes it very easy to set up a map containing rooms that are connected by compass directions. **Pages 3.2 and 3.3** in _Writing with Inform_, “Rooms and the map” and “One-way connections,” explain how to do it, but we’ll take a quick look here, and suggest ways to work through problems that may come up.

>**Where Did It Go?**
>
>The numbering of the Examples in Inform’s Documentation may change in future versions. Likewise the numbering of the pages. However, the names of both Examples and pages should remain the same. If you can’t find a page cross-referenced in this _Handbook,_ consider the possibility that the numbering has changed.

Once you’ve created your first room, you can create more rooms simply by describing the map to Inform, like this:

```inform7
Forest Path is a room. “Tall old trees surround you. The path continues north and south from here.”

Canyon View is north of Forest Path. “The path from the south ends here at the top of a cliff, from which you have a spectacular view of a canyon.”

Haunted Grove is south of Forest Path. “The trees press close around you, moaning faintly and waving their branches in an unsettling way. A path leads north.”
```

This text will create a map with three rooms — from north to south, Canyon View, Forest Path, and Haunted Grove. Inform is smart enough to understand that if you say “Canyon View is north of Forest Path,” Canyon View must also be a room, because rooms and doors are the only things that can be related to other rooms using a compass direction. We haven’t told Inform that Canyon View is a door, so it must be a room.

Inform understands that the connections you have described run both ways. That is, because you’ve said Haunted Grove is south of Forest Path, Forest Path will automatically be mapped north of Haunted Grove. The player who goes south from Forest Path will be in Haunted Grove, and by going north from Haunted Grove the player will return to Forest Path.

>**Capital Offense**
>
>In most situations, Inform is not fussy about whether you capitalize words in your source text. But you can’t use a capital when mentioning map directions in your source (unless the direction is the first word in a sentence). Below are three code examples. The first two work, and produce exactly the same map; the third is a bug, and won’t compile.
>```
>The Lounge is a room.
>The Dining Room is north of the Lounge.
>
>The Lounge is a room.
>North of the Lounge is the Dining Room.
>
>The Lounge is a room.
>The Dining Room is North of the Lounge. [Error!]
>```

The directions you can travel to leave a room are often called the room’s exits. But “exits” is not a term that Inform understands, unless you write some code or include an extension that defines the word.

It’s easy to create room connections that are one-way, or that bend. We’ll show how to do that later in this chapter. A few map connections of this sort may be useful to make your world seem more real, but they tend to annoy players. Players expect that if they traveled from room A to room B using the command E, they should be able to get back to their previous location by typing W.

The room descriptions for Forest Path, Canyon View, and Haunted Grove all tell the player which directions they can travel in when leaving the room. This is a nice way to help the player, though it can make the writing seem a little clumsy. As mentioned earlier, you can download and install an Inform extension (Exit Lister by Eric Eve) that will place the available compass directions in the status line at the top of the game window.

Page 3.2 of _Writing with Inform_, “Rooms and the map,” explains how to deal with a small but sometimes annoying problem in naming rooms and defining map connections: What if you have a room called Hut, and now you want to name a room South Of The Hut? This won’t work:

```inform7
South Of The Hut is south of the Hut. [Error!]
```

Nor will this:

```inform7
South Of The Hut is a room. South Of The Hut is south of the Hut. [Error!]
```

Either of these would work if Inform noticed the way we’re using capital letters, but it doesn’t. The solution is to use the word “called”:

```inform7
South of the Hut is a room called South Of The Hut.
```

This sentence may look as if it was written by Gertrude Stein. (An avant-garde author of the early 20th century, Stein is most famous for the line, “Rose is a rose is a rose.”)

As you can see, Inform’s “natural language” syntax can occasionally be misleading or difficult for humans to read. The sentence makes sense if you read it the right way: South (a direction) of the Hut (a room we’ve already told Inform about) is a room (another room — a new one, this time) called South Of The Hut. This works perfectly, assuming Inform already knows there’s a room called the Hut.

The same problem can arise if we want to call a room something like Inside the Stone House. Inform understands “inside” and “outside” (or “in” and “out”) as directions for travel. So we can’t do this:

```inform7
Inside the Stone House is inside from Haunted Grove. [Error!]
```

Here’s how to do it:

```inform7
Haunted Grove is south of Forest Path. "The trees press close around you, moaning faintly and waving their branches in an unsettling way. A path leads north, and a house built of stone stands here."

Inside from Haunted Grove is a room called Inside the Stone House. The description of Inside the Stone House is "A small, dimly lit room. A doorway to the north leads deeper into the house."
```

Notice the phrase “The description of Inside the Stone House is”. Telling Inform that a description is a description is not usually needed when we define a room, but it is needed here. If we simply start a new sentence with “A small, dimly lit room,” Inform will think we’re giving a description of Haunted Grove. But we’ve already given Haunted Grove a description, so we won’t be allowed to give it another one. The rule is, Inform looks at the _first_ room in the previous sentence (Haunted Grove) and thinks it’s what we’re talking about if we just start a new sentence with a quotation mark. Since we want to write a description of Inside the Stone House, we have to help Inform understand what we have in mind.

If you compile the simple game we’ve been working on so far, which now has four rooms (Forest Path, Canyon View, Haunted Grove, and Inside the Stone House), you’ll find that in Haunted Grove, the travel command IN takes you into the stone house, and OUT gets you back out into Haunted Grove.
