## Creating Things

The most basic way to create a new thing is to tell Inform that it exists:

```inform7
The paintbrush is a thing.
```

This is enough to create an object called the paintbrush. But as yet, the paintbrush is not anywhere in the model world. That is, it won’t appear anywhere when your players/readers encounter your game/story. Sometimes this is what you want: You may need to create objects that are offstage at the beginning of the game, so that your code can move them onstage later. More often, you’ll write an assertion that will cause the thing to appear in a certain place at the beginning of the game. You can do it this way:

```inform7
The Tool Shed is a room.
The paintbrush is in the Tool Shed.
```

Another way to do exactly the same thing is this:

```inform7
The Tool Shed is a room.
The paintbrush is here.
```

I suggest not using “is here,” however. If you need to move paragraphs or whole sections of your code around for any reason, or if you forget how you’ve defined the paintbrush and add more code after the Tool Shed assertion and before the sentence that creates the paintbrush, bad things can happen. (That is, your code may acquire bugs.) It’s safer always to tell Inform specifically where a thing is to be placed at the beginning of the game. This is a safe way to create things, however:

```inform7
The player carries a bowling ball.
The duchess wears a diamond tiara.
```

Inform will understand that both the bowling ball and the diamond tiara are new things that need to be added to the model world. It will also understand that the diamond tiara is **wearable** — that it’s something characters can put on and take off.

Containers and supporters will be discussed in detail later in this chapter. Briefly, a supporter is a thing that acts like a table, so objects can be placed on it. This would also work well:

```inform7
The Tool Shed is a room.
The workbench is a supporter in the Tool Shed.
The screwdriver is on the workbench.
```

Now Inform knows that the screwdriver is a thing, and knows exactly where to put it at the start of the game.

The most important thing about things is that the player can pick them up and carry them around. This is not true of some other types of objects: The player won’t be allowed to pick up a door or a person, for example.

Inform knows almost nothing else about newly created things, though. It doesn’t know the difference between a screwdriver and a bowling ball. In order to have these two things behave in different ways in your game, you’ll have to write some action-processing code. (To learn how to do this, see Chapter 4 of the _Handbook_.)
