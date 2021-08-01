## “You can’t go that way.” {#you-can-t-go-that-way}

A player who tries, in a certain room, to go in a direction for which there is no map connection in that room, will be told, “You can’t go that way.” This message has one advantage: It’s perfectly clear. The player knows not to bother any more trying to go that direction in that room. But it’s not very descriptive. Also, in an open outdoor setting such as a field, being told “You can’t go that way” is unrealistic and rather silly. Fortunately, it’s easy to write more interesting replacement messages:

```inform7
Instead of going nowhere from Forest Path:
        say "You take a few steps into the forest, but deciding it might not be safe, you return to the path."
```

Note that this rule says “going nowhere _from_”. Writing it as “going nowhere _in_” won’t work. However, there are other situations in which the “going ... in” action is needed, and the “going ... from” action won’t work. The basic concept is, “going from” assumes that the action of going has succeeded. In the code above, the player has succeeded … in going nowhere.

This code is fine as far as it goes, but the player will get the same output in response to UP or DOWN, which is not so sensible. We might customize our “You can’t go that way” messages further like this:

```inform7
Instead of going up in Forest Path:
        say "The trees have no branches low enough for you to reach them."

Instead of going down in Forest Path:
        say "There are no gaping holes or open mineshafts in the vicinity."
```

Depending on the features of the rooms in your map, you may want to write custom “You can’t go that way” messages that are different for each room. But we’ll borrow an idea from the next section, on Regions, to suggest a more streamlined approach. After telling Inform that Forest Path, Canyon View, and Haunted Grove are all in a region called Forest Area, we can write Instead rules that will apply across the entire region:

```inform7
Instead of going nowhere from the Forest Area:
        say "You take a few steps into the forest, but deciding it might not be safe, you return to the path."

Instead of going up in the Forest Area:
        say "The trees have no branches low enough for you to reach them."

Instead of going down in the Forest Area:
        say "There are no gaping holes or open mineshafts in the vicinity."
```

If you’re using the Secret Doors extension, you’ll have to do a bit of extra work, because a secret door that hasn’t been revealed will produce the default “You can’t go that way” message, _not_ the custom message you’ve written using an Instead rule like those above. But writing a custom message can be used to give the player an in-the-game clue. Following the code about the secret door in the Doors section, above, you could add something like this:

```inform7
Before going through the oak door when the oak door is unrevealed:
        say "You bump your nose on the oak paneling. Odd -- you had somehow absent-mindedly thought there ought to be a door there.";
        rule succeeds.
```

This message will be output if the player tries to go north through the secret door before it’s revealed.
