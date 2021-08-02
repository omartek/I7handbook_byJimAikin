## Stage Business {#stage-business}

A character will seem more “alive” if she spontaneously does things on her own, or seems to. Sometimes the character will do something that changes the model world (see “Character Actions,” below). But sometimes we just want to print out a reminder to the player — a message that doesn’t actually do anything, but that makes the scene seem more lively. I call these reminder messages “stage business.”

In this example, Janice is the maid. She will seem to do something without really doing anything:

```ìnform7
The Living Room is a room. "This fussy old-fashioned living room is filled with heavy furniture."

Janice is a woman in the Living Room. "Janice is busy tidying up." The description is "Janice is wearing a maid's uniform. She's bustling about, doing all sorts of things."

Every turn when the player is in the Living Room:
        if a random chance of 1 in 3 succeeds:
        say "Janice [one of]flicks dust off of the grand piano[or]runs the vacuum cleaner[or]plumps up the cushions on the sofa[or]straightens a painting[or]polishes the mirror above the mantel[at random]."
```

The Every Turn rule will only run when the player is in the room with Janice. (If Janice were moving around the house, we’d need to change this rule a bit). About 1/3 of the time, a random message will be printed indicating that Janice is busy doing her job.
