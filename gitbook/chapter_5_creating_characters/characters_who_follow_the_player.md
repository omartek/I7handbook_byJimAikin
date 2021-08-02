## Characters Who Follow the Player {#characters-who-follow-the-player}

Writing a character who will find the player and then follow the player around like a faithful puppy is not difficult. Example 39, “Van Helsing” (again on **p. 7.13** of the _Recipe Book_) shows how to do it. We can adapt this code slightly to the example above by getting rid of the code that allows the player to order Bob around, replacing it with this:

```inform7
Bob is a man in Room 3.

Every turn:
        if the location of Bob is not the location of the player:
                let the way be the best route from the location of Bob to the location of the player;
                try Bob going the way;
        otherwise:
                say "'Hey, I'm bored,' Bob says. 'Let's go for a ramble.'"
```

The same suggestion I gave for the “Odyssey” example (just above) applies here. You probably don’t want Bob following the player from the very beginning of the game. To make Bob behave in a way that fits your story, you would need to define a Scene, and then say “Every turn when Too-Friendly-Bob is happening”. Then write a sentence that defines when Too-Friendly-Bob begins.

The extension called Simple Followers, by Emily Short, provides easy ways to create NPCs who will follow the player (or other NPCs) and will start or stop following on command. However, this extension doesn’t work the other way: It doesn’t let the player follow characters who have left the room.
