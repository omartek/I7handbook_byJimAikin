## A Dangerous Jewel Box
The next example shows a way of printing out a single message when the player tries to take several items and is prevented from doing so. There are three jewels in the jewel box, and if the box is in its dangerous state, we want the player character’s fingers to be zapped by an electric shock if he tries to get the jewels from the box. But what we don’t want is an output that looks like this:

```
>take jewels
ruby: Zap! As your fingers near the jewel box, you recoil from a powerful electric shock.
diamond: Zap! As your fingers near the jewel box, you recoil from a powerful electric shock.
sapphire: Zap! As your fingers near the jewel box, you recoil from a powerful electric shock.
```

This would be silly, because the player character would naturally stop after being shocked the first time. Getting the output to read nicely turns out to be complicated, because there are many possible conditions that might occur in the game. The box might be safe rather than dangerous (this is handled in the example with the command TURN CARVING). The player might make the box safe, take two jewels, drop them on the floor, make the box dangerous again, and then try TAKE JEWELS. What should happen then?

The extension Consolidated Multiple Actions by John Clemens, which was recently updated by Emily Short for 6L38 compatibility, can handle this type of scenario — but it only works in Glulx games. If you don’t need or want all of its functionality, studying the code below will show you how to handle this type of situation.

The code below contains comments that explain its logic.

```inform7
The Sultan's Treasure Room is a room. "Awesome treasures surround you! To the north, an arch opens on a balcony."

[To make sure the scoping works properly, we'll add a second room so the tester can carry a jewel or two elsewhere, drop them, and come back:]

The Balcony is north of the Treasure Room. "From here you can see the entire city. The treasure room is back to the south."

The jewel box is an open container in the Treasure Room. "A jewel box sits here, invitingly open. On the front of the box is an intricate ivory carving. In the box you can see [a list of things in the jewel box]." The jewel box can be safe or dangerous. The jewel box has some text called the zap-message. The zap-message of the jewel box is "Zap! As your fingers near the jewel box, you recoil from a powerful electric shock". The intricate ivory carving is part of the jewel box.

[We can make the jewel box safe or dangerous with 'turn carving':]
Instead of turning the carving:
        say "Click -- the carving rotates a quarter-turn to the [run paragraph on]";
        if the jewel box is dangerous:
                now the jewel box is safe;
                say "left.";
        otherwise:
                now the jewel box is dangerous;
                say "right."

A gem is a kind of thing. Understand "jewel" as a gem. Understand "jewels" and "gems" as the plural of gem.

The diamond is a gem in the jewel box. The ruby is a gem in the jewel box. The sapphire is a gem in the jewel box.

[The box only protects jewels. The token can be taken from it at any time:]
The player carries a subway token.

[Taking and removing from are separate actions, so we have to trap them both:]
This is the new announce items from multiple object lists rule:
        if the current item from the multiple object list is not nothing:
                if taking gems when the jewel box is dangerous:
                        do nothing;
                else if removing gems from the jewel box when the jewel box is dangerous:
                        do nothing;
                else:
                        say "[current item from the multiple object list]: [run paragraph on]".

The new announce items from multiple object lists rule is listed instead of the announce items from multiple object lists rule in the action-processing rules.

Before taking gems:
        let L be the multiple object list;
        let N be the number of entries in L;
        [If the player is only trying to take one jewel, the length of the multiple object list will be 0:]
        if N is 0:
        if the noun is in the jewel box and the jewel box is dangerous:
                say "[zap-message of the jewel box]." instead;
        otherwise:
                continue the action;
        [Still here? Then either the player is trying to take several jewels or the jewel box is safe:]
        if the jewel box is safe:
                continue the action;
        [Okay, now we know the jewel box is dangerous, but we don't yet know whether any of the jewels the player aims to take are actually IN the jewel box ... so we'll set up a flag and a list:]
        let danger-present be a truth state;
        let danger-present be false;
        let safe-list be a list of things;
        let safe-list be {};
        [Now let's find out what the player is trying to take:]
        repeat with G running through gems:
                if G is listed in L:
                        if G is in the jewel box:
                                now danger-present is true;
                        otherwise:
                                add G to the safe-list;
        [If none of the jewels the player is trying to take is in the dangerous box:]
        if danger-present is false:
                continue the action;
        [Now we know that at least one of the jewels in the multiple object list is in the dangerous box -- but maybe some of them aren't in the box. In that case, we're going to assume there is no other obstacle, such as inventory management, a greedy hyena, or the player wearing mittens, that would prevent their being picked up. We'll only check to make sure they're in the location:]
        if the number of entries in safe-list is not 0:
                repeat with item running through safe-list:
                        if item is enclosed by the location and item is not carried by the player:
                                now the player carries item;
                                say "[item]: Taken.";
        truncate L to 1 entries;
        alter the multiple object list to L;
        say "[zap-message of the jewel box]." instead;

Test me with "put token in box / take token and ruby / take jewels / take diamond / turn carving / take diamond and ruby / turn carving / drop all / take jewels".
```

The heavy lifting is done by the “Before taking gems” rule. Note that if one or more gems are available for taking, this rule has to handle the process manually. It can’t include, near the end, the line “try taking item”, because that will cause Inform to try running the entire rule again. It will produce a loop, which will result in a run-time error.
