## Achievements {#achievements}

Some authors feel that keeping a numerical score trivializes a serious game, or isn’t interesting from a literary standpoint. Even so, it would be nice to let the player know what kind of progress he or she is making. Instead of producing a numerical score in response to the SCORE command, we can give the player a list of achievements. To do this, we’ll use a table. Tables are one of Inform’s more advanced features, and the syntax for using them is not entirely intuitive. At the end of this example, so as to give you a better grasp of tables, we’ll take a look at how the code works.

We’re going to create a game with three achievements — picking up a ruby, taking off some goggles (which are being worn), and putting a guppy back in the fish tank. These are listed in the Table of Achievements. The table has three columns: object, achievement, and flag. In the object column, we’ll enter the name of the object that is being handled when the achievement happens. In the achievement column is some text describing the achievement. The flag column contains a number; this starts out as 0, but we’ll change it to 1 when the player accomplishes the achievement.

```inform7
The Living Room is a room. The guppy is here. The ruby is here. The player wears some goggles.

The fish tank is an open container in the Living room.

After taking the ruby when the ruby is not handled:
choose the row with an object of ruby in the Table of Achievements;
now the flag entry is 1;
continue the action.

After taking off the goggles:
choose the row with an object of goggles in the Table of Achievements;
now the flag entry is 1;
continue the action.

After inserting the guppy into the fish tank:
choose the row with an object of guppy in the Table of Achievements;
now the flag entry is 1;
continue the action.

Table of Achievements
object        achievement                         flag
ruby          "picked up the ruby"                0
goggles       "removed the goggles"               0
guppy         "put the guppy back in the tank"    0

This is the new announce the score rule:
        let flag-count be 0;
        repeat with N running from 1 to the number of rows in the Table of Achievements:
                choose row N in the Table of Achievements;
                if the flag entry is 1:
                        increase the flag-count by 1;
        if the flag-count is 0:
                say "You haven't done anything notable yet.";
        otherwise:
                let total-flag-count be flag-count;
                say "So far you have [run paragraph on]";
                repeat with N running from 1 to the number of rows in the Table of Achievements:
                        choose row N in the Table of Achievements;
                        if the flag entry is 1:
                                say "[achievement entry][run paragraph on]";
                                decrease the flag-count by 1;
                                if the flag-count is 0:
                                        say ".";
                                        rule succeeds;
                        otherwise if the flag-count is 1:
                                if the total-flag-count is 2:
                                        say " and [run paragraph on]";
                                otherwise:
                                say ", and [run paragraph on]";
                        otherwise:
                                say ", [run paragraph on]".

The new announce the score rule is listed instead of the announce the score rule in the carry out requesting the score rulebook.

Test me with “put guppy in tank / score / take ruby / score / take off goggles / score”.
```

The heavy lifting in this example is done by the new announce the score rule, which replaces the announce the score rule (one of the Standard Rules). The new rule does two things. First, it uses a loop (“repeat with N running from 1...”) to count the number of achievements the player has so far done. Each time it finds a row where the flag is 1, it increases the flag-count. Then it prints out a message. If the flag-count is still zero, nothing has been accomplished, so the rule will say so and stop.

If the flag-count is at least 1, that means the player has done something. In this case we start the printout by saying, “So far you have [run paragraph on]”. Then we go through the Table of Achievements again, looking for and listing achievements. As we go, we decrease the flag-count — but we’ve taken the precaution of storing it in total-flag-count before the process starts. This is so we’ll know whether the list is exactly two items long, or whether it’s longer. If it’s exactly two items long, we want to print “ and ” between them, but if it’s three or more items long, we want to print “, and ” between the last two. This is the serial comma. If you’re not using the serial comma in your game (see [here](../chapter_1_getting_started/writing_your_first_game.md#from-the-top)) you can omit the lines that use total-flag-count.

For more ways to report scoring, see the examples on **p. 11.4**, “Scoring,” in the _Recipe Book._
