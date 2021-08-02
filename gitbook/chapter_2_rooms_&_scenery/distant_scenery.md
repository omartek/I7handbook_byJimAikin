## Distant Scenery

It often happens, as you write a room description of an outdoor “room,” that you’ll want to mention things that are far away — visible, but not something that can be interacted with. Inform has no built-in way to handle this situation, but we can easily create one.

We’ll start by showing the problem, and then show how to fix it. Here is our first attempt at source code:

```inform7
The Forest Path is a room. "Tall old trees surround you. The path continues north and south. In the distance to the west, off among the trees, you can see a crumbling stone wall."

The crumbling stone wall is scenery in the Forest Path. "The wall is ancient and moss-covered." Understand "ancient" and "moss-covered" as the stone wall.
```

This code is fine, up to a point. The player can now examine the wall. But while the room description indicates that the wall is off in the distance, Inform doesn’t know that. The result, when the player tries doing things with the wall, is less than great:

```
>x wall

The wall is ancient and moss-covered.

>touch wall

You feel nothing unexpected.

>take wall

That's hardly portable.
```

Obviously, the player character wouldn’t be able to touch the wall, because it has been described (in the room description) as far away. To solve this problem, we’re going to create a new **property**. Objects in Inform can have many properties. (You can view the properties of any object in the Game panel by typing SHOWME and the name of the object.) The printed name and description are properties, for instance. And creating new properties is easy. Let’s create an either/or property called distant/near. Every object in the model world will be either distant or near, but all of them will be near unless we say otherwise:

```inform7
A thing can be distant or near. A thing is usually near.

Instead of doing anything other than examining to a distant thing:
        say "[The noun] [are] too far away."

The crumbling stone wall is scenery in the Forest Path. "The wall is ancient and moss-covered." Understand "ancient" and "moss-covered" as the stone wall. The stone wall is distant.
```

After creating distant as a property, we can make the stone wall (or anything else) distant, just by saying that it is. Now the output will be a lot more sensible:

```
>touch wall
The crumbling stone wall is too far away.
```

The code above assumes that the distant thing will always be the first object the player refers to in an input. That is, it will be the _direct object_ of the verb. In Inform source code, the direct object is referred to as the **noun**. If there’s another noun later in the command (usually it would be in a prepositional phrase), you would refer to it in your source as the **second noun**.

To be safe, we might also want to trap commands like PUT VASE ON STONE WALL. In this command, the stone wall is the second noun. To handle this, you can write:

```inform7
Instead of doing anything when the second noun is a distant thing:
        say "[The second noun] [are] too far away."
```

This code won’t work well if the command involves, for instance, talking to an NPC about a distant thing. ASK GUARD ABOUT STONE WALL might produce the output, “The stone wall is too far away.” In fact, this will only happen if we’ve written our game so as to allow the ASK ABOUT action to refer to actual things, not just to topics. The way to do this is explained in Chapter 5, in the section “Topics of Conversation” [here](../chapter_5_creating_characters/conversations,_part_ii_asktellgiveshow.md#topics-of-conversation). But wanting to exclude certain actions from an “Instead of doing anything” rule might come up in other situations too, so we’ll dig into it here. After creating an action called quizzing about, as explained in that section of Chapter 5, we could allow distant things to be quizzed about like this:

```inform7
Instead of doing anything other than quizzing someone about something when the second noun is a distant thing:
        say "[The second noun] [are] too far away."
```

If you’re reading closely, you may wonder why the code above uses “[are]”, and why this produces the word “is” when you test the game. This is one of the newer features of Inform. We’ll have more to say about this type of text substitution in Chapter 9\. The point of doing it this way is that Inform is smart enough to tell whether the object under discussion is singular or plural. It will select “is” or “are” as needed. If we just wrote, “[The second noun] is too far away”, distant things that were plural-named, such as geese winging across the sky, wouldn’t work quite right. We’d see this:

```
>touch geese
The geese is too far away.
```

With the geese, we might prefer to create a distant thing called the flock of geese, and not make it plural-named (since “flock” is singular). A herd of cows could be handled the same way. But if you get in the habit of using this type of text substitution when writing default messages that may have to apply to a number of different objects, your game will read much more smoothly.

For a more complex way of creating an outdoor environment that includes items in other locations, see “Indoors &amp; Outdoors” in Appendix B of this book.

At this writing, Jon Ingold’s Far Away extension, which is designed specifically to deal with things that are too far away to be touched, has not been upgraded for 6L38 compatibility. To learn how to update it (and other extensions), turn to Appendix B.

Once you’ve edited Far Away, it will do what we’ve been discussing in this section. Just put

```inform7
Include far Away by Jon Ingold.
```

near the top of your source code and then write a sentence saying that the crumbling stone wall is distant. With the extension in place, you won’t need to write your own Instead rules to produce “too far away” messages. You may want to do so for particular literary reasons. For example:

```
>touch moon
The moon is much, much too far away!
```

But you won’t need to do that unless you want to.
