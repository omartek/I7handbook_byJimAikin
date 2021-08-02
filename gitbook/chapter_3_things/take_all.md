## Take All

Since the TAKE ALL command came up in the section on “Looking Under &amp; Looking Behind,” we may as well take a quick look at how to deal with it. Experienced IF players have a tendency to type TAKE ALL whenever they enter a new room, just to see what’s lying around that isn’t nailed down. This is a useful command, and many players feel it’s their right to be able to use it. If you disable it entirely, some players may not be happy with your game. Earlier versions of Inform tried to let the player take even scenery objects (after which the player would learn that the scenery objects were not portable) and people (leading to a report that the person wouldn’t care for that). This was all rather silly. In the current version of Inform (and most likely in the future as well), TAKE ALL does not include people or scenery. This is described on **p. 18.36** (“Deciding whether all includes”) of _Writing with Inform._

We might decide to let “all” include a particular scenery item, perhaps because the player’s attempt to take it will reveal something interesting. Unfortunately, page **18.36** fails to provide a correct explanation of how to re-include something in ALL. Here’s the correct way to do it:

```inform7
The billiard table is scenery in the Recreation Room.

Instead of taking the billiard table:
        say "It's much too heavy for you to pick up, but when you try to lift it, it rocks slightly, as if the floor beneath it is uneven."

Rule for deciding whether all includes the billiard table while taking or taking off or removing: it does.
```

We have to include the list of actions (taking or taking off or removing) because the Inform compiler assembles its lists of the rules in your game in a particular way (as discussed in the next chapter). More specific rules are listed before rules that are more general (less specific). The library’s rule for TAKE ALL lists those actions, so if we fail to mention them in our rule, our rule will be placed _after_ the standard “rule for deciding whether all includes scenery”. If our customized rule is placed after the standard rule rule, our rule will never be used.
