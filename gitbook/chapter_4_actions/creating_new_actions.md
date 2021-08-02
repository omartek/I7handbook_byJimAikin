## Creating New Actions {#creating-new-actions}

To create a new action, we need to do three things:

1.  We give the action itself a name, so that we’ll be able to refer to it in our code.

2.  We tell Inform exactly what forms of input will cause the action to happen, using Understand rules.

3.  We write some code that tells Inform exactly what to do when the action happens. (This would include both things that happen if the action succeeds, and messages that will print out if the action fails for some reason.)

Chapter 6 of the _Recipe Book,_ “Commands,” has a lot of good information on how to create your own actions. If you haven’t read this yet, give it a look.

To illustrate the various possibilities for creating actions, we’re going to create an action that will happen when the player uses the verb PAINT. Painting is not an action that’s built into Inform, but painting something might be a way of solving a puzzle in your game.

The most basic form of this action is one that takes no nouns at all — the bare command PAINT. We can create it this way:

```inform7
The Test Lab is a room. "Many devious tests are conducted here. You can see a wooden fence."

A wooden fence is scenery in the Lab.

Painting is an action applying to nothing. Understand "paint" as painting.

Check painting:
        say "You don't have any paint." instead.
```

If you compile this game and test it, you’ll see the following output:

```
>paint
You don't have any paint.

>paint the fence
I only understood you as far as wanting to paint.
```

The painting action as we’ve defined it does nothing at all: The check rule has no exceptions. We could, however, make an exception if we wanted to, using an Instead rule. For instance, we might do this:

```inform7
Check painting when the location is the Paint Store:
        say "You find it impossible to choose from among the hundreds of tempting colors." instead.
```

Most often, we’d expect the player to want to paint some particular thing, so the example above is included mainly to illustrate the simplest way to create a new action, one that has no noun. We’ve defined the action (“Painting is an action applying to nothing.”) We’ve told Inform what inputs will trigger the action (“Understand “paint” as painting.”) And we’ve written a Check rule that will run when the painting action is being processed. Because we haven’t defined any grammar that would match the command PAINT THE FENCE, the parser reports that it has failed: “I only understood you as far as wanting to paint.”

It’s important to remember that by default, a Check rule does _not_stop the processing of the action. After the Check rule runs, the Carry Out, After, and Report rules for the action will all run — unless one of them stops the process. To prevent this, if you want action processing to stop after your check rule, tack the word “instead” on at the end of the say phrase you’re printing out in the Check rule. As you might guess, this causes the Check rule to operate more like an Instead rule, and Instead rules fail by default, so after your Check rule has run, action processing will halt.

Next, let’s look at how to paint something. This example is going to get complicated, because in order to actually do any painting we’ll need, at the very least, a paintbrush, and quite likely a can of paint as well. But we can start by creating the action we’ll need. Remember, we’ve already created an action called painting (which applies to nothing), so we can’t call our new action painting. Let’s call it paint-applying:

```inform7
Paint-applying is an action applying to one thing and requiring light. Understand "paint [something]", "put paint on [something]", and "apply paint to [something]" as paint-applying.

Check paint-applying:
        say "[The noun] [look] fine the way [they] [are]."
```

The odd-looking stuff with square brackets in the Check rule’s say line cleverly formats the output text as singular (“The wooden fence looks fine the way it is.”) if the noun is singular, and as plural (“The galoshes look fine the way they are.”) if the noun is plural.

As before, this action does nothing except print out an error message. But now PAINT THE FENCE will produce a sensible output.

The essential thing to notice is the use of the grammar token “[something]” in the action’s Understand sentence. The token “[something]” will match any object that is in scope — that is, any object that is visible to the player character. This is the heart of creating new actions in Inform.

The phrase “and requiring light” in the definition of the action is useful mainly if your game includes any dark rooms. Painting is obviously an action that requires light, so if the player is in a dark room we want to make sure she can’t paint anything, even if she does have all of the necessary painting implements.

The next thing we need to do, of course, is to add a painting implement, specifically a paintbrush, so that the player can type PAINT FENCE WITH PAINTBRUSH. For this tutorial, I’m not going to bother adding a paint can that the brush needs to be dipped into. This brush comes fully loaded with paint, which is not very realistic, but it will simplify the code in the examples.

When creating an action that requires two nouns, it’s a very good idea to give the action a name that includes “it with”, “it on”, “it under”, or some similar phrase. In this case, we’re going to create an action called “painting it with”. Giving the action this type of name — “xxxxing it with” — is not required, but if you forget to do it, your code will be hard to read, and you’ll probably have more bugs to fix. In some cases, you might need to use a different preposition. For instance, you might need to create an action called “unfastening it from” or “placing it near”.

Here is a fairly complete bunch of code that includes all three of our new painting actions. As you’ll see, the Check rule has a fairly deep and tangled set of indentations. If you’re trying out this game, you’ll need to copy these with care. Even better would be to develop an understanding of how indentation works in Inform. For information on this, turn [here](../chapter_9_phrasing_&_punctuation/indenting.md#indenting).

```inform7
The Test Lab is a room. "Many devious tests are conducted here. You can see a [wooden fence]."

A wooden fence is scenery in the Lab. The description is "It's a [if the fence is painted]freshly painted[otherwise]plain[end if] wooden fence." The wooden fence can be painted or unpainted. The wooden fence is unpainted. Understand "freshly" and "painted" as the wooden fence when the wooden fence is painted. The printed name of the wooden fence is "[if the fence is painted]freshly painted [end if]wooden fence".

A paintbrush is in the Lab. Understand "brush" as the paintbrush.

Painting is an action applying to nothing. Understand "paint" as painting.

Check painting:
        if the player carries the paintbrush:
                say "You'll need to be more specific about what you want to paint.";
        otherwise:
                say "You don't have any paint."

Paint-applying is an action applying to one thing and requiring light. Understand "paint [something]", "put paint on [something]", and "apply paint to [something]" as paint-applying.

Check paint-applying:
        if the noun is the fence:
                if the fence is painted:
                        say "You already did that.";
                otherwise if the player carries the paintbrush:
                        try painting the fence with the paintbrush instead;
                otherwise:
                        say "You'll need to find a paintbrush somewhere if you want to do that.";
        otherwise:
                say say "[The noun] [look] fine the way [they] [are]."

Painting it with is an action applying to two things and requiring light. Understand "paint [something] with [something]" as painting it with.

Check painting it with:
        if the second noun is not the paintbrush:
                say "[The second noun] can't be used for painting things." instead;
        otherwise if the player does not carry the paintbrush:
                say "You'd need to find a paintbrush somewhere if you want to do that." instead;
        otherwise if the noun is not the fence:
                say "[The noun] [look] fine the way [they] [are]." instead;
        otherwise if the fence is painted:
                say "You already did that." instead.

Carry out painting it with:
        now the fence is painted.

Report painting it with:
        say "You apply a fresh coat of paint to the fence."
```

This code is written in a way that assumes the player will never need to paint anything except the wooden fence. If several objects in the game can be painted, it would have to be changed. In that case, we might want to use Instead rules for each paintable object rather than Carry Out and Report rules. The code could be expanded in other ways. For instance, we might want to change the color of the fence after it’s painted. But this example should give you a better idea how to create a new action.

You might notice a couple of other things too. We’ve allowed the fence to be either painted or unpainted. This is a new property we’ve created, which exists only for the fence object. This is so we can give the player an error message if he tries to paint the fence more than once. We’ve added some vocabulary words to the wooden fence object (“freshly” and “painted”) that can only be used by the player after the fence is painted.

We’ve also told Inform that the printed name of the fence (the name printed out when the game runs) depends on whether it has been painted. Finally, the room description refers to “[wooden fence]”, so the room description will change after the fence is painted.

You may want to study the logic of the Check rule for painting it with. It’s important to get the if-tests in a sensible order. The first question is, is the second noun something other than the paintbrush? If so, print an error message and stop (using the “instead” to stop the action processing). If the second noun _is_ the paintbrush, we then ask, has the player neglected to pick up the paintbrush? (It might be locked up in the glass case, or just lying on the ground.) Next, we check whether the noun is something other than the fence. If not — if the player is indeed trying to paint the fence — then the fourth question to ask is, is the fence painted already? Only if the answers to all four of those questions are “No” will the action processing move on to the Carry Out rule.

If these four questions are in some other order, the output might not be so sensible. If we put the question of whether the fence is painted first, for instance, this output could happen:

```
>paint the bucket with the apple
You already did that.
```

Trust me, players will sometimes try absurd commands like that, just to see what will happen. If they’re beta-testing your game, that’s what you _want_ them to do. When creating a new action, it’s a good idea to think about all of the silly things a player might try. What happens if she tries to perform the action on herself? On another character? On something she’s wearing?

I tested the code above at least a dozen times while writing it. I tried all of the absurd inputs as I could think of, such as PAINT FENCE WITH APPLE, just to see what would happen. When writing a new action, you’ll want to go through quite a bit of testing yourself before letting your trusted team of testers try torturing the game.
