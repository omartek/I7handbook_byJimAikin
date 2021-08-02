## Giving Orders that Involve Going Elsewhere

At times, you might want the player to be able to give an NPC an order that requires going somewhere else and doing something there. The basic difficulty in this case is, in effect, that once the NPC has gone somewhere else, he or she can’t “hear” the player character. A secondary difficulty, which will arise once we solve the first one, is that when the NPC is carrying out an action in a different location, the parser will report it to the player, even though the NPC is invisible. The solution to the latter requires the extension called Scope Control, by Ron Newcomb. (Ron also contributed to the development of this example.)

Here’s a simple game in which the player can order Jeeves the butler to go somewhere else and do something — specifically, go north, get the cheese, and then go south again.

```inform7
Include Scope Control by Ron Newcomb.

The Dining Room is a room. The Kitchen is north of the Dining Room.
Jeeves is a man in the Dining Room. There is a cheese in the Kitchen.

A persuasion rule for asking someone to try doing something:
        persuasion succeeds.

The block giving rule is not listed in the check giving it to rules.

The subject is a person that varies.

Before asking someone to try doing something:
        now the subject is the person asked.

Before reading a command: now the subject is the player.

After deciding the scope of the player while parsing for persuasion:
        place the subject in scope.

Unsuccessful attempt by someone doing something when the location of the actor is not the location:
        do nothing.

Before answering someone that something when the location of the noun is not the location, stop the action.

Test me with "Jeeves, n then get cheese then s then give me the cheese".
```

In a real game, we probably wouldn’t want to use such a sweeping persuasion rule. The variable called “the subject” is changed to Jeeves when the player gives Jeeves an order. Then the subject is placed in scope. As a result, Jeeves will “hear” all of the orders even when he’s in a different room. The two last rules (Unsuccessful attempt and Before answering someone) prevent Jeeves’ actions from being reported if he’s in a different room.
