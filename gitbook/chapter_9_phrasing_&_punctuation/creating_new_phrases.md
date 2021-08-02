## Creating New Phrases

Sometimes you may need to have your game do several things at once. A good way to take care of this is to write what other programming languages would call a _function_. This feature of Inform is introduced on **pp. 11.2 and 11.3** of _Writing with Inform._ Writing a function in Inform is easy — just use the word “To”, like this:

```inform7
To sound the alarm:
        now the alarm horn is blasting;
        now the burglar is frightened;
        now the guard dog is awake;
        [...and so on...]
```

From anywhere else in your code, you can now sound the alarm, simply by telling Inform that that’s what you want to do:

```inform7
if the burglar carries the jewels:
        sound the alarm.
```

The main reason to write a function of this sort would be if your game may need to sound the alarm from several different places in the code, in response to several different events. Rather than putting the “sound the alarm” code in several places, you can put it in just one place. This way, if you need to edit it later, you only need to make the change in one place, which is easier and also reduces the chance of introducing a bug into your game.

If you need to, you can write a function that can be applied to any number of different objects in your game. Here’s a slightly artificial example that shows the syntax:

```inform7
To blast open (box - a container):
        now the box is open;
        now the box is not openable;
        now the box is damaged;
        say “Boom! You blast open [the box].”
```

The word “box” in this example is a temporary name for some data (in this case, an object that is a container) that is sent to the “To blast open” phrase. In order to run this block of code, you would have to tell Inform what “box” will refer to. If your game includes an old trunk and a safe, for instance, you could write a line saying “blast open the old trunk” or “blast open the safe” in your code. When Inform calls the “To blast open” function in response to a line that reads “blast open the old trunk,” it will know that the old trunk is now the “box” being referred to, so it will operate exactly as if you had written “now the old trunk is open”, “now the old trunk is not openable”, and so on. At the end, the game will report, “Boom! You blast open the old trunk.”

But if you mistakenly try to blast open something that isn’t a container, you’ll have a bug. It’s also important to note that the code above changes the property called “damaged” on the container. If you forget to create the property “damaged” for all of the containers in your game, the code above may cause a run-time error.

Take another look at the syntax in the code above. To write a function that takes an argument (or two arguments, if you need to), you use parentheses, create a temporary name for the argument (“box”), then use a single hyphen with spaces around it, then tell Inform what kind of argument you’re planning to send to the function.
