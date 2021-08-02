## Testing Conditions

Many of the examples in this book test conditions in the model world and produce a different result depending on the conditions. The keyword in each case is “if”. **Page 11.6** of _Writing with Inform_ (“If”) explains how to create and test conditions. The point of testing a condition is for the game to make a decision about what to do next. If the condition is true, we want the game to do one thing; if the condition isn’t true, we want something different to happen. Here’s a simple example:

```inform7
if the player carries the big stick:
        end the story saying “You have won!”;
otherwise:
        end the story saying “You have failed.”
```

Just to be clear, this code can’t stand on its own. It has to be embedded in a rule, so that Inform will know when to perform the test. For instance, something like this:

```inform7
Every turn when the player is in the Cave:
      if the player carries the big stick:
            end the story saying “You have won!”;
      otherwise:
            end the story saying “You have failed.”
```

Inform is a bit unusual in that it also allows us to test a condition using “unless”. Unless means the opposite of if:

```inform7
unless the player carries the big stick:
        end the story saying “You have won!”;
otherwise:
        end the story saying “You have failed.”
```

The condition being tested in those examples was “carries”, but we can test almost any condition — is, wears, and so on. We can test whether a truth state is true or false, or whether a property of an object has a certain value. For instance, if we’ve written that temperature is a kind of value, and that the temperatures are frigid, tepid, lukewarm, and boiling hot, and also told Inform that the sea has a temperature, then we could test the temperature of the sea like this:

```inform7
if the sea is boiling hot:
        say "Look! Pigs with wings!"
```

Two or more if-tests can be strung together in one line, like this:

```inform7
if the cat is on the couch and the catnip is on the couch and the dog is not on the couch:
        say "The cat goes a little crazy."
```

But in this type of construction, Inform insists that each phrase in the if-test be spelled out in full. The condition shown below makes perfect sense to a human reader, but the syntax is too complicated for Inform to understand:

```inform7
if the cat and the catnip are on the couch: [Error!]
```
