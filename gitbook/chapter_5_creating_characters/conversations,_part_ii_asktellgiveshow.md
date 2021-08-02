## Conversations, Part II: ask/tell/give/show {#conversations-part-ii-ask-tell-give-show}

Personally, I favor the ask/tell/give/show conversation system. (Other game authors disagree.) I feel it gives a good compromise between realism and challenging the player to figure out what’s important and therefore worth having a conversation about.

This system is based on five commands:

```
ASK NPC ABOUT X
TELL NPC ABOUT X
SHOW X TO NPC
GIVE X TO NPC
ASK NPC FOR X
```

The give to, show to, and ask for actions are included in Inform. To use them in their basic form, all you need to do is write a few Instead rules. The ask about and tell about actions are included in Inform in a limited way: You can ask about or tell about topics (which are just strings of text), but not about objects that exist in the game unless you set up topics that have the same vocabulary as the objects. We’ll take a close look at all of these commands, and show ways to make them more flexible.

The simplest command to add to your game is give to. Continuing the earlier example game, with Troy in the Billiard Room, we can do this:

```inform7
The player carries a plum.

In the Billiard Room is a hammer.

Instead of giving the plum to Troy:
        say "Troy inspects the plum carefully, accepts it, and pops it into his mouth.";
        remove the plum from play.

Instead of giving something to Troy:
        say "Troy sneers at you. 'I'm not interested,' he says coldly."
```

If you add this code to your game, you’ll discover a couple of things. First, Troy will eat the plum, but will sneer at any other gift you may offer. (And incidentally, Inform knows that “offer” is a synonym for “give”.) Second, if you try GIVE HAMMER TO TROY, the parser will cause you to pick up the hammer first before the giving action is attempted. This is called implicit taking. It’s a handy feature, because it saves the player a bit of trouble: You don’t need to PICK UP THE HAMMER first before giving it to Troy. (See the Action Processing Summary [here](../chapter_4_actions/action_processing__summary.md#action-processing-summary) to learn a bit more about implicit actions.)

If the implicit taking fails (for instance, if you try to give an NPC a canary when the canary is in a locked cage), the giving action will never be attempted. Inform assumes that the PC can only give something to an NPC while actually holding it.

This makes sense for the giving action (though you’d need to write some extra code in order to allow the player to give an NPC a poisonous snake while the snake is curled up inside a cage). But the same condition applies to the showing action, and here it makes a bit less sense. What if I want to show an NPC the beautiful sunset? By default, Inform will try to have the player take the sunset first, and of course that won’t work.

We can get around this limitation by writing a Before rule (instead of an Instead rule), like this:

```inform7
Before showing the tuxedo to Troy:
        say "'Yes,' he replies sarcastically. 'I've already noticed that I'm wearing it.'" instead.
```

Now you can show the tuxedo to Troy without having the parser try to have you take the tuxedo (which of course Troy won’t let you have).

### Topics of Conversation {#topics-of-conversation}

Inform’s default handling of ASK ABOUT and TELL ABOUT is good in one way, but bad in another way. These commands are implemented so as to handle topics, but they don’t know about objects in the game. Let’s suppose we want the player to be able to ask Troy about that interesting tuxedo. Here’s the basic way to do it:

```inform7
Instead of asking Troy about "tuxedo":
        say "'Oh, you've noticed my tuxedo,' he replies. 'I'm rather fond of it.'"
```

This is fine as far as it goes. The good news is, we can ask Troy about abstract topics, such as the meaning of life, using exactly the same syntax. The meaning of life doesn’t have to be an actual object in our model world. The disadvantage is that the parser will only match the _exact_ word or words in the topic. A quick look at the output will show why this can be a big problem:

```
>ask troy about tuxedo
"Oh, you've noticed my tuxedo," he replies. "I'm fond of it."

>ask troy about the tuxedo
There is no reply.
```

The Instead rule above didn’t include “the tuxedo” as a text, and Inform has no idea that the topic “the tuxedo” is the same as the topic “tuxedo.” Topics are not handled with the same kind of automatic intelligence as objects, because it wouldn’t be practical for the parser to do so.

We can get around this limitation in a couple of ways. First, we can do it by letting Inform know about all of the ways we think the player might refer to the tuxedo. But it quickly gets a bit awkward:

```inform7
Understand "tuxedo", "the tuxedo", "his tuxedo", "suit", "the suit", and "his suit" as "[tuxedo]".

Instead of asking Troy about "[tuxedo]":
        say "'Oh, you've noticed my tuxedo,' he replies. 'I'm rather fond of it.'"
```

Here we’ve created a new grammar token, “[tuxedo]”, and provided an understand rule that spells out the words and phrases we want the player to be able to use. But of course, the careful author will already have given a vocabulary list to the tuxedo itself:

```inform7
Troy is wearing a tuxedo. The description of the tuxedo is "Troy's tuxedo is a handsome bit of custom tailoring." Understand "Troy's", "handsome", "custom", "tailoring", "suit", and "attire" as the tuxedo.
```

Wouldn’t it be nice if we could use that same vocabulary list while asking or telling Troy about the tuxedo? Inform lets us do this, and with only a bit more work. We need to create two new actions, quizzing it about and informing it about. These will use the same command words (ask and tell) as Inform’s built-in actions, but we’ll set them up to respond to “[something]”, that is, an in-game object, instead of an abstract topic.

```inform7
Quizzing it about is an action applying to two things. Understand "ask [someone] about [something]" and "quiz [someone] about [something]" as quizzing it about.

Check quizzing it about:
        say "[The noun] shrugs unhelpfully."

Informing it about is an action applying to two things. Understand "tell [someone] about [something]" and "inform [someone] about [something]" as informing it about.

Check informing it about:
        say "'That's interesting,' [the noun] says, stifling a yawn."

Instead of quizzing Troy about the tuxedo:
        say "'Oh, you've noticed my tuxedo,' he replies. 'I'm rather fond of it.'"
```

Notice that we’ve changed the Instead rule so that it now applies to the quizzing it about action, not to the built-in asking it about action. Now the player can ask and tell any character about any object in the model world, and use or not use THE in the input.

But there’s still one big limitation we have to be aware of: The grammar token “[something]” will only match things that are visible in the room — that is, objects that are in scope. If we want to be able to ask and tell characters about objects that are not present, we need to change “[something]” in the grammar for our new actions to “[any thing]”. We also need to change the definitions of our actions so that instead of applying to two things, they apply to one thing and one visible thing.

The reason for the latter change may not be obvious, but if you try editing your code to refer to “[any thing]” but don’t change “thing” to “visible thing”, you’ll see that the action doesn’t work properly. **Important concept:** Technically, “a thing” is shorthand for “a currently visible, touchable thing”. That’s what you’ll be typing most often, so Inform lets you save a little typing. But when you say “visible thing,” Inform understands that you’re referring to something that’s visible somewhere or other in the world, whether or not it’s touchable. This may seem backwards, because — well, it _is_ backwards.

Here are the final versions of our new actions:

```inform7
Quizzing it about is an action applying to one thing and one visible thing. Understand "ask [someone] about [any thing]" and "quiz [someone] about [any thing]" as quizzing it about.

Informing it about is an action applying to one thing and one visible thing. Understand "tell [someone] about [any thing]" and "inform [someone] about [any thing]" as informing it about.
```

Using this code, we can let the player ask characters about any object in the model world. We can also create, if we like, offstage things that can be used for conversation. These things don’t need to be anywhere in the model world, and they don’t need any properties other than their vocabulary:

```inform7
Weather is a thing. Understand "clouds", "rain", and "wind" as weather.
```

But the idea of talking to an NPC about something that’s not in scope raises a new complication: What if the NPC has never seen the object and thus knows nothing about it? For that matter, what if the player character has never seen the object (or at least, not in this particular run-through of your game) and thus doesn’t officially know that it exists? To deal with these questions, we need a way to track characters’ knowledge.

Fortunately, there’s already an extension package that does some of the heavy lifting for us. Now that you’ve learned the basics of how to create an ask/tell/give/show conversation system, you can forget about the details unless you happen to need them for some reason. Download and install Conversation Responses by Eric Eve. This extension provides a simpler way to write conversation topics. It also lets you write greetings and farewells.

I also like Eric’s Conversational Defaults (which requires his Conversation Framework, so you’ll need to download and install that too, along with his Epistemology extension, which tracks what the player character knows about). Conversational Defaults makes it easier to set up default responses, which will be printed out in the game when you haven’t written a response for a specific ask or tell action. With only a little effort, you can use Conversational Defaults to make your characters seem somewhat more lifelike than if the player only encountered the standard line, “There is no reply.” With Conversational Defaults, we can give an NPC a bunch of possible outputs when he or she doesn’t have a real response, and instruct Inform to select a response at random. Here’s a short sample game that shows how to do this:

```inform7
Include Conversational Defaults by Eric Eve.

The Test Lab is a room. The description is "Many devious tests are conducted here."

The zombie is a man in the Lab. "There's a dead guy sort of standing here. A zombie, from the look of him." The description is "The zombie looks really ill. Really, really ill." Understand "dead", "guy", "man", and "ill" as the zombie.

default ask-tell response for the zombie:
        say "[one of]The zombie shrugs minimally[or]The zombie scratches his cheek and grunts unintelligibly[or]'I can't remember hardly anything,' the zombie says[or]The zombie only leers at you menacingly for a moment before sliding back into his usual morose lethargy[at random]."
```

The effect we’re creating above — having the zombie give a variety of different “non-responses” when asked or told about something for which the author hasn’t written a real response — goes a long way toward making an NPC seem a bit more real.

If your story needs a lot of conversation, you might also want to consider the extension Threaded Conversation by Chris Conley. This is a complex and sophisticated package based on earlier work by Emily Short. Among other things, it provides a method for the author to suggest topics of conversation to the player during the story, in a smooth and context-sensitive way. For instance, the story might suggest, “You could ask Dave about the lighthouse or the police van.” After the player has asked Dave about the lighthouse, it would disappear from the suggestions, leaving only the police van — unless some new topic had been revealed by Dave’s reply about the lighthouse, in which case the next conversation prompt might be, “You could ask about the police van or the flying reptiles.”
