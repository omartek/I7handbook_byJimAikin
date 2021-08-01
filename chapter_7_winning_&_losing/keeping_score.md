## Keeping Score {#keeping-score}

In a game whose story is serious in tone, awarding points might seem too frivolous, so you might want to use no scoring. Inform allows the author, however, to give the player points for doing certain actions. A way to do this is explained on **p. 9.2** of _Writing with Inform_, “Awarding points.” The first step is to put this line near the top of your source code, along with whatever other Use or Include options you’ve selected:

```inform7
Use scoring.
```

Among its other effects, this line will cause the current score to be displayed alongside the turn count in the banner at the top of the game window. Normally, you would award points in an After rule, like this:

```inform7
After taking the gold crown for the first time:
increase the score by 10;
say "Ah, you've finally gotten your hands on it!"
```

Unless we include “continue the action” at the end of the After rule, the After rule will halt the action processing _before_ the Report rule has a chance to tell the player that taking the gold crown has succeeded. So if you’re not going to print out a message of your own when awarding points, you’ll want to add the line “continue the action” after awarding the points. This will cause the Report rule to report “Taken”, “You put the bulb in the socket”, or whatever.

When awarding points, you should get in the habit of always including the phrase “for the first time” in the rule that awards the points. If you forget to do this, the player will be able to rack up a huge score by performing the same action over and over!

Having explained that, however, I’m now going to suggest that you not do it that way. The reason is because the phrase “for the first time” applies only the first time the player _attempts_ to do something, whether or not it succeeds. So if the gold crown is in a locked transparent display case and the player tries TAKE CROWN while the case is still locked, no points will be awarded, but later, when the case is unlocked, taking the crown still won’t award any points, because now it’s not the first time the action has been attempted.

It’s much safer to use one of Inform’s built-in properties, **handled,** to check whether points should be awarded:

```inform7
After taking the gold crown when the gold crown is not handled:
```

Use “for the first time” to award points _only_ when you can be sure that the action will succeed the first time the player attempts it.

Examples 136 and 137 in _Writing with Inform_, “Mutt’s Adventure” and “No Place Like Home,” show other ways of awarding points. **Page 9.3**, “Introducing tables: rankings,” shows how to create a table of rankings that will tell the player how well he or she is doing. This feature was popular in early IF games, and some authors still enjoy using it.

Inform doesn’t insist that the number of points awarded for an action be constant. If you like, you can do this:

```inform7
crown-points is a number that varies. crown-points is 10.

After taking the gold crown when the gold crown is not handled:
        increase the score by crown-points;
        say "Ah, you've finally got your hands on it!"
```

If you’ve set it up this way, you can vary the number of points the player will gain for taking the crown depending on what else has happened in the game. You can even award a negative number of points, thus reducing the player’s overall score. In my first game, “Not Just an Ordinary Ballerina” (which was written in Inform 6, not Inform 7), I set up a system that would reduce the number of points the player could gain by solving each puzzle based on the number of hints the player had consulted about that puzzle. The only way to get the maximum score for winning the game was never to consult the hints. This was meant to give players an incentive to use their ingenuity rather than relying on the hints.

If your game has scoring, it’s a good idea to keep a list somewhere of how many points are being awarded for each scored action. Add up the total possible score. Near the top of your source code, tell Inform the maximum score, as suggested on **p. 9.2**, “Awarding Points”:

```inform7
The maximum score is 12.
```

### A Treasure Chest {#a-treasure-chest}

Awarding points when an object is picked up or a room entered is the usual thing to do in a game. But some classic games require that the player put the objects that have been found in a treasure chest or trophy case. Awarding points for this action is slightly tricky, because the treasure chest might be a closed openable container. If it happens to be closed the first time the player tries to put a given treasure into it, the points will never be awarded. Consider this code:

```inform7
The Lab is a room.
The player is carrying a fish.
The old shipping trunk is a closed openable container in the Lab.

After inserting the fish into the trunk for the first time:
        increase the score by 1;
        continue the action.
```

That certainly looks as if it should work. But here’s the output:

```
>put fish in trunk
The old shipping trunk is closed.

>open trunk
You open the old shipping trunk.

>put fish in trunk
You put the fish into the old shipping trunk.

>score
You have so far scored 0 out of a possible 0, in 4 turns.
```

No points were awarded for putting the fish in the trunk, because the first time the player tried it, the trunk was closed. Here’s the correct way to write the After rule:

```inform7
After inserting the fish into the trunk:
        if the fish is in the trunk for the first time:
                increase the score by 1;
        continue the action.
```

But wait ... what if we want the player to be awarded points only while the treasure _remains_ in the treasure chest? This requires a slightly different approach. What we need to do is award a point each time the treasure is successfully inserted into the treasure chest, and also subtract a point each time the treasure is taken out of the chest. To subtract a point, just increase the score by -1\. Here’s one way to do that, using the example of the fish and the old trunk, as before:

```inform7
After inserting the fish into the trunk:
        if the fish is in the trunk:
                increase the score by 1;
        continue the action.

Instead of taking the fish:
        if the fish is in the trunk:
                decrease the score by 1;
        continue the action.
```

This use of an Instead rule assumes that there are no active Check rules that would subsequently prevent the taking of the fish; Instead runs before Check in the action processing. In most cases it should work for you.
