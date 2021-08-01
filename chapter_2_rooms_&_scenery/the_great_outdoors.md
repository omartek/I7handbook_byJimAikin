## The Great Outdoors {#the-great-outdoors}

Earlier in this chapter, in the section “Distant Scenery,” we looked at how to make distant scenery items that could be examined but not interacted with in any other way. But it’s also possible that when you’re creating an outdoors area, you’ll want the player to be able to use commands like ‘look north’ to be able to inspect what’s in the distance. And if there are any objects in the game that are large enough to be seen from a distance, it would be natural to want the output of a ‘look north’ command to mention them.

In addition, once a large object has been brought to the player’s attention in this way, you might want the player to be able to examine it, even if the result is something like, “Professor Plum is too far away for you to make out any detail.” This requirement is a bit tricky to code, because as far as Inform is concerned, things that are in other rooms are not in scope, which means the player won’t be able to refer to them at all. Or rather, the player is free to refer to them, but the parser will pretend they don’t exist.

If you want to write a realistic outdoor setting, spend some time studying Chapter 3.4, “Continuous Spaces and the Outdoors,” in the _Recipe Book_. The examples there illustrate some powerful techniques. Here we’ll take a quick look at a couple of them. First, a slight revision of the “Distant Scenery” example. We’re going to create a couple of distant scenery objects. We’ll give them names that start with “view-of-” so that Inform won’t confuse them with the real objects in other locations.

```inform7
A thing can be distant or near. A thing is usually near.

Instead of doing anything other than examining to a distant thing:
        say "[The noun] [are] too far away."

The Forest Path is a room. "Tall old trees surround you. The path continues north and south. In the distance to the west, off among the trees, you can see a low stone wall."

The winding path is scenery in Forest Path. "The path meanders from north to south."

The view-of-wall is privately-named scenery in the Forest Path. "The low stone wall appears to be ancient and moss-covered." Understand "wall", "low", "stone", "ancient" and "moss-covered" as the view-of-wall. The view-of-wall is distant. The printed name of the view-of-wall is "stone wall".

By the Wall is west of the Forest Path. "A crumbling stone wall runs from north to south here, blocking the way to the west. To the east, among the trees, you can see a path."

The crumbling stone wall is scenery in By the Wall. "The wall is ancient and moss-covered." Understand "ancient" and "moss-covered" as the stone wall.

The view-of-path is privately-named scenery in By the Wall. "The path is only faintly visible from here, meandering among the trees to the east." The view-of-path is distant. Understand "meandering", "path", and "trees" as the view-of-path. The printed name of the view-of-path is "path among the trees".
```

Next, we’ll allow the player to look in a direction:

```inform7
Direction-looking is an action applying to one visible thing and requiring light. Understand "look [direction]" as direction-looking.

Carry out direction-looking:
        say "You see nothing unusual in that direction."
```

Next, we’ll create a response when the player looks in a direction where we’ve placed some interesting scenery:

```inform7
Instead of direction-looking west in the Forest Path:
        say "There's a low stone wall off in the distance to the west."
Instead of direction-looking east in By the Wall:
        say "To the east, a path meanders from north to south among the trees."
```

But what if the player has dropped something large in the other location? Ideally, we’d like it to be mentioned when the player looks in that direction. This requires a few more steps. Near the top of the code for the game, we do this:

```inform7
A room has some text called the containing-name. The containing-name of a room is usually "".
```

To test the functionality we’re going to add, we’ll need an object large enough to be visible from a distance:

```inform7
A thing can be huge. A thing is usually not huge.
The beach ball is in Forest Path. The beach ball is huge. The description is "Red and white." Understand "red" and "white" as the beach ball.
```

Next, we’ll give our outdoor rooms containing-names, and add a function that will use this property:

```inform7
The containing-name of the Forest Path is "Lying on the path".
The containing-name of By the Wall is "Not far from the wall".

To scrutinize (R - a room):
        let L be a list of things;
        repeat with item running through things in R:
                if item is huge:
                add item to L;
        if the number of entries in L &gt; 0:
                say " [The containing-name of R] you can see ";
                say "[L with indefinite articles].";
        otherwise:
                say "[line break]".
```

The final step is to revise the code for direction-looking so as to take advantage of the scrutinizing function:

```inform7
Instead of direction-looking west in the Forest Path:
        say "There's a low stone wall off in the distance to the west.[run paragraph on]";
        scrutinize By the Wall.
Instead of direction-looking east in By the Wall:
        say "To the east, a path meanders from north to south among the trees.[run paragraph on]";
        scrutinize the Forest Path.
```

With these additions, when we go west to By the Wall and LOOK EAST, we’ll get this output:

```
>look east
To the east, a path meanders from north to south among the trees. Lying on the path you can see a beach ball.
```

> **The “The”**
>
>If you know a little about Inform programming, you might think that because the view-of-wall object created in the example above is privately-named and has a printed name, the code could just as easily read “View-of-wall is privately-named scenery...”, rather than, “The view-of-wall is privately-named scenery....” Since the name “view-of-wall” will never be used, why should the “The” make the slightest difference?
>
>It does, though. If you omit the “The” when writing a paragraph that creates an object, Inform will assume that the object is proper-named. (An example of how this mechanism is designed to work would be if you create an object by saying, “Bob is a man in the Gazebo.” Inform correctly infers that the object called Bob is proper-named, so it will never construct an output sentence that refers to “the Bob.”) The compiler will make this assumption even if the object is privately-named. As a result, substitution strings such as “[The noun]” in your text output code won’t work properly if you omit the “The”. Normally, this substitution will produce “The wall” in the output, or “Bob”, as needed. The “The” (either capitalized or not) is suppressed with proper-named objects. So if you forget the “The”, you’ll see ugly outputs like “wall is too far away.”

One problem remains. The beach ball is being mentioned (because it’s huge), but the command X BALL will produce the output “You can’t see any such thing.” True, there’s not much to see, because the beach ball is far away, but it would be nice if the parser didn’t produce such a confusing output. To fix it, we would need to play with the scoping rules. Fortunately, Example 365 in the Documentation, “Stately Gardens,” which is part of the “Continuous Spaces and the Outdoors” page in the _Recipe Book_, shows exactly how to do this, so we don’t need to go into it here. The solution begins with some code that looks something like this:

```inform7
The Great Outdoors is a region. The Forest Path and By the Wall are in the Great Outdoors.
After deciding the scope of the player when the player is in the Great Outdoors:
        repeat with the way running through directions:
                let next-room be the room the way from the location;
                if the next-room is a room:
                        place the next-room in scope.
```

More detail would be needed to produce a convincing illusion of the great outdoors, but this should give you an idea of what’s required: Objects in adjacent rooms have now been added to scope, which means the parser will recognize them when the player refers to them. They can now be examined (but nothing else) from adjacent rooms in the region. For a more complete implementation, with which the player can throw things in a direction and have them sail away out of sight, see “Indoors &amp; Outdoors” in Appendix B.
