## A Word About Fairness

In the early days of interactive fiction, numerous games were released that would kill the player without warning. That was part of the fun (?) — when you opened a door, maybe an ogre would jump out at you and hit you with his club, and the game was over. If you had been smart enough to save your game position not too long before, you could restore the saved game and try to be more careful about the ogre the second time. If you hadn’t been smart, you might have to spend hours getting back to that game position again.

Today, many players and authors feel that this type of story event is more annoying than fun. The trend is to give the player some sort of advance warning, which might be subtle or obvious, when the player character is about to get in a dangerous spot. “Dark red stains have seeped into the floorboards around the door” in the room description would be a good way to warn the player that opening the door could be dangerous, and that looking around for a way to do it cautiously would be a good idea.

It’s all too easy to write a game, even without meaning to, in such a way that the player can make the game unwinnable. For instance, the player may need to give the chocolate biscuit to the elf so that the elf will be willing to part with the silver key … but the biscuit might be edible, and the player might have eaten it a hundred moves before meeting the elf. Another example: Maybe the player can’t return to a region of the map after leaving it. A rope bridge might have fallen the first time the player crossed it, leaving no way to get back across the canyon. If the player dropped the gold key on the far side of the bridge, she won’t be able to go back and get it. If the gold key is required to open something that’s on _this_ side of the canyon, the game has become unwinnable.

You need to think carefully about where in your story this type of problem can arise, and decide how you want to handle it. Drawing a diagram of the flow of the story — of the puzzle structure, in other words — may be helpful.

One way to handle the situation is to simply not allow the player to do anything that would make the game unwinnable. If the chocolate biscuit will be needed later, write something like this:

```inform7
Instead of eating the chocolate biscuit, say "It's a mouth-watering treat, no doubt, but you decide to save it for later."
```

It can be a chore to come up with sensible-sounding reasons why the player character wouldn’t do something, if it seems a perfectly natural thing to want to do. After all, the player can’t read your mind, and doesn’t know what actions or objects will later be needed to win the game. For variety, I sometimes allow the player to do something that will turn out to make the game unwinnable, but then add an immediate message giving a broad hint (which the player is free to ignore) that that was probably a stupid thing to do:

```inform7
After eating the chocolate biscuit:
        say "You chow down on the delicious biscuit and lick the last of the chocolate from your fingers. Afterward, though, you start to worry. Maybe you shouldn’t have indulged your gluttonous impulses quite so casually.";
        rule succeeds.
```

The player who reads this will probably be smart enough to UNDO the latest action, thereby retrieving the chocolate biscuit.
