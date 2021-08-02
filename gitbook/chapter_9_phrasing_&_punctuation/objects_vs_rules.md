## Objects vs. Rules

Many computer programming languages are firmly based on the idea of objects. Even if you’re creating something as abstract as an email program, every button or icon on the screen and every window that opens will probably be a separate object within the software. The technical definition of “object” doesn’t matter at the moment: You can just think of a software object as a bunch of related code.

As you write with Inform, you’ll be creating lots of software objects. Usually these will correspond to objects in the model world. A tree, for instance, would almost always be modeled using an object. In fact, it would be a _thing,_ which is a kind of object. But Inform is unusual in that it isn’t as object-oriented as many programming languages. If you have some experience programming in another language, you may be dismayed at first to find that some types of data can be created either as free-floating global values or as properties of objects.

It really doesn’t matter which type of data you use, because all of the data properties of objects are public. They have global scope. (If you’ve never done any object-oriented programming, this paragraph will make no sense to you. Feel free to ignore it.) Also, objects in Inform don’t have methods. All functions are global, although they can be written in such a way as to apply only to one object.

Instead of calling methods on objects, Inform uses rules and rulebooks. When you write rules in Inform, for the most part you can put them wherever you’d like in the source. When your game is compiled, Inform will collect all of the rules you’ve written and all of the rules in the extensions you’ve included, and assemble them all into rulebooks.

When a rulebook is consulted during gameplay, Inform will proceed downward through the list of rules in the rulebook. When it finds a rule that applies to the current action, it will follow the rule. If the rule makes a decision (that is, if it ends with “rule succeeds”, “rule fails”, or “stop the action”), Inform will stop. Otherwise, it will continue on through the rulebook, and then perhaps proceed to other rulebooks in the action-processing sequence, as shown on **p. 12.2** of _Writing with Inform._

The rulebooks are constructed by the compiler according to certain principles. If you’re curious how this works, you should definitely read **Chapter 19** of _Writing with Inform_, “Rulebooks.” Basically, rules that are more specific will be listed earlier in the rulebook, while more general rules will be listed later. For instance, a game might have these two rules:

```inform7
Instead of inserting something into an open container:
        [...more code would go here...]

Instead of inserting something into the coffee cup:
        [...more code...]
```

When Inform constructs the Instead rulebook, it will put the rule about inserting into the coffee cup _before_ the rule about inserting into an open container, because the rule about the coffee cup is more specific — it relates only to one object, not to any container that has the open property. When the game is being played, the Instead rule for the coffee cup will be consulted first. It will (presumably) end with a default “rule fails”, so action processing will halt. The rule about inserting something into an open container will never be reached.

As **p. 18.4** of _Writing with Inform_ (“Listing rules explicitly”) explains, we can tinker with the ordering of the rules if we need to. We can tell Inform to put a rule first or last in a rulebook, or before or after some other specific rule (if the latter rule has a nam). If a rule has a name (and most of the rules in Inform’s Standard Rules have names), we can unlist them like this:

```inform7
The can't exceed carrying capacity rule is not listed in any rulebook.
```

Or we can replace an existing rule with our own named rule, like this:

```inform7
The new carrying capacity rule is listed instead of the can't exceed carrying capacity rule in the check taking rulebook.
```

If you need to figure out which rules (either the rules in the Inform library, or rules in an extension, or new rules that you’ve written) are causing a certain output in a situation in your game, use the RULES command and then inspect what happens when you give the command that causes that output. You can also open Inform’s Standard Rules using the Open Extension command in Inform’s File menu, and search for specific words — but whatever you do, _don’t edit this file!_ The details of Inform’s Standard Rules have been worked out through years of deep thought, trial-and-error, and highly technical bug reports from experienced authors. Even small changes will quite likely cause bad things to happen.

The only reason to open the Standard Rules, other than simple curiosity, would be to replace it. To do this, (1) copy the rule, (2) paste it into your code, (3) give it a new name, (4) edit it as needed in your code, and then (5) replace the old rule with your newly edited version using code like the line shown above. Doing this is safe, and it’s occasionally necessary, but it’s not something to try until you’ve learned a lot about Inform — and even then, it’s not something to do casually.

Unfortunately for those who are curious about how the Standard Rules operate, some of them simply refer to underlying code in Inform 6, which is not to be found in the Standard Rules. The manner in which the Inform 7 compiler uses Inform 6 code is not something we can reasonably get into in this _Handbook_, as it’s probably the most advanced topic in Inform programming.

The Rules tab in the Index has some very nice tools for looking at the rules in your game. You can even remove many of the Standard Rules by clicking the “unlist” button, which will insert a line of code into your game. Again, this is not an action to take casually, as the result could be that your game misbehaves quite seriously in response to player input. But it’s a useful tool to have when you need it.
