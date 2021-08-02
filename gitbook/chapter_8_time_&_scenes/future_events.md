## Future Events {#future-events}

**Page 9.11** of _Writing with Inform_, “Future events,” shows how to cue up events that will happen at a certain time in the future. For the next example, I’ll borrow some code from the chapter of the _Handbook_ on characters. When the player tries to take the spider, not only the game prevent the action, but there will be an after-effect — a sort of emotional echo of the intended action:

```inform7
Instead of taking the spider:
        say "You can't bring yourself even to get near it.";
        the spider thought returns in four minutes from now.

At the time when the spider thought returns:
        say "You're still thinking about that creepy spider...."
```

Here I’ve created a new phrase, “the spider thought returns,” and told Inform what to do when that event happens. There are two ways to cue this action: You can say “in four minutes from now” or “in four turns from now” (substituting your own number of turns or minutes, obviously). If you’re making adjustments in the time of day, as shown earlier in this chapter in the section “Passing Time,” four minutes from now will _not_ necessarily be the same as four turns from now. The handy thing about this code is that the spider thought time will be reset if the player tries to take the spider several times in a row: The thought return will happen only once. If the player then tries to take the spider _after_ the thought has returned the first time, the thought can return a second time.

If you need to trigger a more complex series of events rather than something that happens once, using Scenes (see below) will give you better tools.

If you want something to _maybe_ happen in the future, depending on some factor, you can use Inform’s handy “do nothing” phrase. The example below was suggested by one of my students, who wanted to transform a magic wand into an old shoe — but only if the player has been carrying the wand for three turns in a row.

```inform7
The Wizard's Workshop is a room. "This odd-smelling little room is crowded with tables and shelves overflowing with magical implements."

The magic wand is in the Wizard's Workshop. "A Wham-O(tm) magic wand lies on the floor." The description is "It's a shiny black plastic wand on which the words 'Wham-O' are written in flowing white script." Understand "wham-o", "shiny", "black", and "plastic" as the magic wand.

The old shoe is a thing. The description is "It looks like somebody left it lying in the gutter."

After taking the magic wand:
        the wand transforms in three turns from now;
        continue the action.

At the time when the wand transforms:
        if the player does not carry the wand:
                do nothing;
        otherwise:
                remove the magic wand from play;
                now the player carries the old shoe;
                say "The wand quivers and squirms in your hand! Suddenly it's not a wand, it's an old shoe!"
```

Here, we start Inform’s internal “alarm clock” ticking when the player takes the magic wand, using an After rule. If the player isn’t carrying the wand when the “alarm clock” goes off, nothing happens. And if the player drops the wand and picks it up again, Inform will automatically reset the clock. The wand will only transform if it’s carried for three turns in a row. Obviously, this type of scheduling of future events has many other uses. In the code above, the transformation can occur only once, because the wand ends up off-stage as a result of the transformation. If you’re planning to use teleportation (moving the wand somewhere interesting) rather than transformation, you’ll need to think closely about what happens if the player triggers the event again later.
