## Loops

Sometimes a computer program needs to perform a certain operation over and over. If it needs to do the same operation 50 times, there’s no sense in writing out the same block of code 50 times. Instead, we write it out once and then execute it over and over until we’re done. The process of doing this is called a loop.

Loops are used less in interactive fiction than in many other types of programming, but they definitely have their uses. The basic syntax for how to use loops is on **p. 11.9** (“While”), **p. 11.10** (“Repeat”),and **p.** **11.11** (“Repeat running through”) of _Writing with Inform_. We’ve already seen loops a few times in the _Handbook,_ for instance [last script here](../chapter_9_phrasing_&_punctuation/values.md#values), where the loop was used to move a bunch of dollar bills. Here’s a more straightforward example.

Let’s suppose you have a set of rooms in a region called the Underground Area, and let’s suppose the player has just thrown a circuit breaker that plunges the entire Underground Area into darkness. In that case, you could write a routine in which you manually list each room in the Underground Area and make it not lit — but it would be easier, and less likely to introduce errors, if you write a routine that automatically loops through all of the rooms in the Underground Area and makes them dark, like this:

```inform7
Carry out switching off the circuit breaker:
        repeat with R running through rooms in the Underground Area:
                now R is not lit;
        continue the action.

Carry out switching on the circuit breaker:
        repeat with R running through rooms in the Underground Area:
                now R is lit;
        continue the action.
```

In these two Carry Out rules, we’re using the temporary variable R to refer to a room. (We could just as easily have called it Freddie — the use of R to mean “room” is not special.) The loop is created by the word “repeat”. To execute the loop, Inform first makes a list of the rooms in the Underground Area and then runs the code for the loop (which in this case consists of the single line “now R is not lit”) a number of time. Each time Inform goes through the loop, the variable R refers to a different room. So the loop has the effect of turning off the lights in each room in the Underground Area, one by one. When it gets to the end of the list of rooms in the Underground Area, the loop stops.

Here’s a slightly more complete example that uses a while loop. Inform provides no command with which the player can empty out a container, so we’ll create one. We’ll also give the player a container that can be emptied.

```inform7
The player carries a basket. A spool is in the basket. A squirrel is in the basket. A pencil is in the basket. A banana is in the basket.

Emptying is an action applying to one thing. Understand "empty [something]" as emptying.

Check emptying:
        if the noun is not a container:
              	say "That's not something you can empty." instead;
        else if the noun is not open:
              	say “You’ll need to open [the noun] first.” instead;
        else if nothing is in the noun:
              	say "There's nothing in [the noun]." instead.

Carry out emptying:
      	let R be a random thing in the noun;
      	while R is not nothing:
            		move R to the location;
            		now R is a random thing in the noun.

Report emptying:
        say "You dump out the contents of [the noun] onto the floor."

Test me with "x basket / empty basket / l / empty basket / empty pencil".
```

The loop is in the Carry Out Emptying rule. (The check rule makes sure that the object the player wants to empty is a container, that it’s open, and that it’s not empty already.) We first create a temporary variable, R, and assign its value to something or other in the container (we don’t care what). We have to do this before we enter the while loop, so that Inform will know what R refers to. After moving R to the location, we make R stand for something else, and then we return to the top of the loop. As long as R is something (an object), the loop will continue to cycle. But if the container is now empty, R has become nothing, so the loop terminates.
