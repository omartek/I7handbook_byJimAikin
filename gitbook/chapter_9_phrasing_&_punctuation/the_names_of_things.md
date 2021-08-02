## The Names of Things

When you create a thing in your model world, the name you give it is understood by both the compiler and the parser. Most of the time, this is a convenient feature. But once in a while you may want to override it. You can do this using the **privately-named** and **printed name** properties. If you’ve read Chapter 2 of this Handbook, you may recall that we looked at a problem that can crop up if you try to name a room using a direction word. If you have a room called Hut, for instance, creating another room called South of the Hut is possible, as explained on **p. 3.2** of _Writing with Inform_, “Rooms and the map,” but it’s awkward.

I prefer to do it this way:

```inform7
South of the Hut is Hut-South-Side. The printed name of Hut-South-Side is "South of the Hut".
```

This will work nicely, but if you do it this way, you’ll have to call the room Hut-South-Side each and every time you mention it in your code.

While we’re at it, we’ll put a thing in this room:

```inform7
The object22 is a privately-named thing in Hut-South-Side. The description is "It's a beautiful little yellow flower." Understand "beautiful", "little", "yellow", and "flower" as object22. The printed name of object22 is "yellow flower".
```

This object can’t be referred to by the player as “object22”, because it’s privately-named. In this case, there would be no reason not to simply call the object “yellow flower” in your own code. But in some situations, creating a privately-named object might be useful. If you do so, remember to also give it a printed name.

As **p. 4.10** of _Writing with Inform_ “Conditions of things”) shows, you can add variable output to a printed name. Here are two ways to do it, either of which might be useful in some situations:

```inform7
The printed name of the ceramic bowl is "[bowl-condition] ceramic bowl".

The printed name of the ceramic bowl is "[if broken]broken [end if]ceramic bowl".
```
