## Values {#values}

Values in Inform are pretty much like what other computer programming languages call _variables_. And in fact, when we create a value we can either call it a variable, or say that it varies:

```inform7
X is a number variable.
Y is a number that varies.
```

But as **p. 4.8** (“New value properties”) and the following pages of _Writing with Inform_ show, many of the values authors use in Inform programming are not numbers but words or even blocks of text:

```inform7
X is a text variable. X is "Ugh."
Y is a text that varies. Y is "Wow!"
```

After creating the values above (X and Y), we can _initialize_ them if we like by telling Inform what to store in the value at the start of the game. The statements “X is “Ugh.”” and “Y is “Wow!”” should be read as starting with an invisible “When play begins:”. They’re not permanent assignments — the data stored in X and Y can change during the game. What we can’t do is change the _kind_ of data stored in the value. Elsewhere in our code, we could say “now X is “Okay, I guess....””, but we couldn’t say “now X is 17”, because that would attempt to turn X from a text into a number.

What’s extremely interesting and useful for game design is that Inform’s word values can have properties. If you look at **p. 4.9**, you’ll see these two statements:

```inform7
Brightness is a kind of value. The brightnesses are guttering, weak, radiant, and blazing.
A brightness can be adequate or inadequate. A brightness is usually adequate. Guttering is inadequate.
```

Why would you want to do this? Because now you can test whether the brightness of a thing is adequate:

```inform7
A lamp is a kind of thing. A lamp has a brightness. The brightness of a lamp is usually radiant. The table lamp is a lamp.
```

Now we can write a test such as, “if the brightness of the table lamp is adequate”.

Values that are lists of words can be changed explicitly (“now the brightness of the table lamp is weak;”), but you may occasionally want to change the value without knowing beforehand what it is — for example, if the player needs to set a furnace or a loudspeaker to a higher or lower level. When we do this, we have to be careful. First the syntax, then the explanation:

```inform7
now the brightness of the table lamp is the brightness after the brightness of the table lamp;
```

The reason this can be problematical is because Inform assumes that the named values are arranged in a circle. The brightness after radiant is blazing (which is fine), but the brightness after blazing is guttering. As a result, the player who turns up the lamp repeatedly may find that it suddenly stops producing light. This is not very desirable. To squash this kind of bug, we need to take a different approach. Continuing to work with the brightness of the table lamp, we might do something like this:

```inform7
To promote the brightness of (X - a thing):
        if the brightness of X is not blazing:
        now the brightness of X is the brightness after the brightness of X.

To demote the brightness of (X - a thing):
        if the brightness of X is not guttering:
        now the brightness of X is the brightness before the brightness of X.
```

Now we can safely boost the lamp’s brightness in our code by writing, “promote the brightness of the table lamp.” For more about this syntax, see **p. 11.18** of _Writing with Inform,_ “The value after and the value before.”

In addition to variable values, Inform includes what programmers call _boolean_ values. A boolean variable can have only one of two possible values: It’s either true or false. Inform calls this type of variable a **truth state**. Often it’s easier to use named value properties rather than truth states, but sometimes a truth state will do the job more succinctly. Here are two ways to accomplish pretty much the same thing:

```inform7
The ceramic bowl can be broken or unbroken. The ceramic bowl is unbroken.

The ceramic bowl has a truth state called brokenness. The brokenness of the ceramic bowl is false.
```

If we do it the first way, we can later test “if the ceramic bowl is broken”. If we do it the second way, we need to test “if the brokenness of the ceramic bowl is true”. That’s a slightly more cumbersome way to phrase the code.

In some programming languages, you could write, “if the brokenness of the ceramic bowl:”, and the language would understand that because brokenness has to be true or false, this if-test is sensible, and should be evaluated as either true or false. But Inform won’t do this. We have to write, “if the brokenness of the ceramic bowl is true:”.

More information on values is found on **p. 8.1** and **p. 8.4** (“Change of values that vary” and “Change of either/or properties”) of the Documentation.

When you create a value and attach it to an object as a property of that object, you should always tell Inform what value to give the property at the start of the game. This is called _initializing_ the value:

```inform7
The drill bit is a thing. The drill bit has a number called length. The length of the drill bit is 6.
```

(If you want to have the length be in inches, centimeters, or some other unit of measurement rather than just a number, consult **p. 15.8** of _Writing with Inform_, “Units.”) You don’t actually have to initialize the value of a number, but if you don’t, your game may not work the way you expect it to.

If you’re creating a kind of object — something that you’ll have several of in your game — you can give every instance of the kind the same property. Again, initializing the value is a good idea:

```inform7
A drill bit is a kind of thing. A drill bit has a number called length. The length of a drill bit is 6.

The iron bit is a drill bit. The length of the iron bit is 4.
```

Another way to do this is to create a kind of value and then give the object that kind of value:

```inform7
Hardness is a kind of value. The hardnesses are hard and soft.
A drill bit is a kind of thing. A drill bit has a hardness. The hardness of a drill bit is hard.
```

This doesn’t prevent you from creating some particular drill bit with a hardness of soft; all the code above is really saying is that the hardness of a drill bit is _usually_ hard (unless you happen to write something that changes it). Experienced Inform programmers use the word “usually” in this situation:

```inform7
The hardness of a drill bit is usually hard.
```

You can say “The hardness of a drill bit is always hard.” The word “always” produces a constant value, one that can’t be changed elsewhere in your code.

Temporary, local values can be created within code blocks. If you’re new to programming, you may not realize that these temporary values have meaning _only_ within the code block where they’re defined. Once that block finishes, the value is thrown away. For instance, here’s some code borrowed from Chapter 5 of this book:

```inform7
After reading a command:
        let T be text;
        let T be the player's command;
        [... and so on ...]
```

The word “let” is used to create a temporary value (that is, a variable). Here, we’ve created a temporary value called T. In this situation, we don’t need to tell Inform that T is a value that varies; Inform understands that it will probably need to vary while the After rule is running. What you need to know is that T can’t be referred to anywhere else in your code. It exists only within this After rule. In fact, you can write many different rules that have values with the same name, such as “X” or “the nearby room”. This doesn’t produce a bug.

Within the code block, you can manipulate the temporary value in whatever way you might like — but your manipulations will have an effect on the rest of the model world only if you write some code that causes them to. If you need to store a temporary value that you’ve created within a code block in order to be able to use it later on in some other part of the program, you can do so by creating a permanent variable as a storage space:

```inform7
The drill bit has a number called length. The length of the drill bit is 4.
Instead of drilling the hole:
        let L be a number;
        let L be the length of the drill bit;
        [...some other code here changes the temporary value L...]
        now the length of the drill bit is L.
```

Here’s an example of what can happen if you forget that a “let” value in a code block is temporary. The person who posted the question in the rec.arts.int-fiction newsgroup wanted to figure out how much money the player had in her wallet; and if there was enough money, to pay out some of it. Can you spot the bug in this code?

```inform7
A dollar bill is a kind of thing. The description of a dollar bill is "It's an ordinary greenback." Understand "dollars" as the plural of dollar bill. Understand "greenback" as a dollar bill.

The player carries a wallet. The wallet is an open container. In the wallet are 20 dollar bills. The description of the wallet is "Leather, and rather the worse for wear."

Bribing is an action applying to one thing and requiring light. Understand "bribe [someone]" and "pay off [someone]" as bribing.

Instead of bribing the inspector:
        if the player carries the wallet:
                let d be the number of dollar bills contained in the wallet;
                if d is less than 10:
                        say "You don't have enough cash to bribe the inspector.";
                otherwise:
                        change d to d minus 10;
                        say "After bribing the inspector, you have [number of dollar bills contained in the wallet] dollars remaining."
```

The output is this:

```
>bribe inspector
After bribing the inspector, you have 20 dollars remaining.
```

We’re told the inspector has been bribed to the tune of $10, but no money has actually left the wallet. The problem is that the code only manipulates the value of d, which is a temporary local variable. It never actually removes the dollar bill objects from the wallet. But in fact the problems with this code run a bit deeper. What if the player character has $20 available, but has already removed $12 from the wallet and is holding them in his or her hand, leaving only $8 in the wallet? In that case, the Instead rule will fail when it ought to succeed. And what if the player has $7 in hand and $8 in the wallet? We still need to extract $10, but we don’t initially know where the bills are located.

We need to revise the Instead rule rather extensively. Using a little literary license just for fun, we might come up with the code below, which works as desired. Note that the actual handling of the dollar bills is done in repeat loops. For more on loops, see [here](../chapter_9_phrasing_&_punctuation/loops.md#loops).

```inform7
Instead of bribing the inspector:
        let c be the number of dollar bills carried by the player;
        let d be 0;
        if the player carries the wallet:
                	now d is the number of dollar bills contained in the wallet;
        let total be d plus c;
        if total is 0:
                	say "A hurried inventory [if the player carries the wallet]of your wallet [end if]reveals that you're flat broke. 'I would never resort to offering you a bribe,' you say haughtily. But the inspector is unimpressed. 'In that case,' he says, 'you'll be payin['] the city a hefty fine. That's how the game is played, guy.'";
        otherwise if total is less than 10:
              	if d is greater than 0:
                    		[if the player has any money at all in the wallet, it will be removed and offered to the inspector, who will turn it down:]
                    		repeat with X running from 1 to d:
                          			let greenery be a random dollar bill in the wallet;
                          			now the player carries greenery;
                    		say "You haul some money out of your wallet and hold it out [run paragraph on]";
              	otherwise:
              		      say "You hold out every dollar you have [run paragraph on]";
              	say "to the inpector in a trembling hand, but he only favors you with a disgusted look. 'Not enough,' he says. 'Not near enough.'";
        otherwise:
              	[We don't know whether the player has 10 or more dollars in hand, or whether some of the dollars need to be transferred from wallet to hand before being used -- all we know is that between the in-hand dollars and the wallet dollars, there are enough. So we'll start by adding to the in-hand dollars if we need to:]
              	if c is less than 10:
                    		repeat with X running from c to 9:
                          			[Yes, 9 is correct. If c is 7, for instance, we need 3 more, so we want the loop to run 3 times -- once with X being 7, once with it being 8, and finally with it being 9:]
                          			let greenery be a random dollar bill in the wallet;
                          			now the player carries greenery;
                    		say "You flip open your wallet. [run paragraph on]";
              	repeat with X running from 1 to 10:
                    		let greenery be a random dollar bill carried by the player;
                    		remove greenery from play;
              	say "'Would ten dollars be enough to have you ignore the bare wires, the cracks in the foundation, and the gaps in the pipe joints?' you ask, holding out the cash. 'Oh, sure, heck, whatever,' the inspector replies. In a moment the transaction is concluded. He makes a few careless check marks on his clipboard and moves away, humming a little tune. 'Pennies from Heaven,' it sounds like.";
              	remove the inspector from play.
```
