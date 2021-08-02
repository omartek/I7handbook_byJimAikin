## The Omega Machine

This sophisticated example showed up back in 2009 on the intfiction.org forum. The author, who goes by the handle SJ_43, was responding to a question from someone named Eudoxia about how to make a device that the player can give commands to — for instance, a command like COMPUTER, CHECK THE STABILIZERS. The game below doesn’t implement anything quite that complicated, but it provides a framework with which you could easily do it. The sneaky Inform 6 trick in this code is the line, “Include (- has talkable, -) when defining a computer.” The parentheses and dashes are used (as described [here](../chapter_10_advanced_topics/special_features_in_glulx.md#special-features-in-glulx)) to drop the code out of I7 and down into I6. “has talkable” is I6 code that means, more or less, “This is an object the player may want to be able to talk to.”

Note that the Default Messages extension may change or not be compatible with a future version of Inform 7\. It’s used here to create a special error message for devices of the computer kind.

I’ve customized SJ_43’s code by adding some calendar messages for Omega. In a real game, you’d probably want to store such messages in a table, so as to be able to refer to different messages at different points in the game.

```inform7
A computer is a kind of device.
Include (- has talkable, -) when defining a computer.

Checking for mail is an action applying to nothing.
Understand "mail", "display mail", and "show mail" as checking for mail.

Check an actor checking for mail:
      	unless the actor is a computer, stop the action.

Carry out a computer checking for mail:
      	say "'You have no messages.'"

Displaying the calendar is an action applying to nothing.
Understand "calendar", "display calendar", and "show calendar" as displaying the calendar.

Check an actor displaying the calendar:
      	unless the actor is a computer, stop the action.

Checking for mail is doing computer stuff. Displaying the calendar is doing computer stuff.
Persuasion rule for asking a computer to try doing computer stuff: persuasion succeeds.

Instead of doing computer stuff, say "That command is for computers only."

Instead of a switched off computer (called comp) doing something:
      	say error message for the comp;
      	rule succeeds.

Asking a computer about something is computer conversation.
Telling a computer about something is computer conversation.
Asking a computer for something is computer conversation.
Instead of computer conversation, say "You can only do that to something animate."
Instead of answering a computer that something, say error message for the noun.

To say error message for (comp - a computer):
      	if comp is switched on, say "'Does not compute!'";
      	otherwise say "[The comp] is currently switched off."

The Lab is a room. Omega is a computer in the Lab. Understand "pda" as Omega. The description of omega is "Your trusty handeheld pda.  The chrome-plated device is voice-activated, and no batteries are necessary since it has a built-in microfusion reactor."

Carry out Omega displaying the calendar:
	     say "[one of]'You're late for your appointment with the white rabbit!' says Omega[or]'Time for a flu shot!' says Omega[or]'I'm afraid I can't do that, Dave,' says Omega[or]'No appointments today,' says Omega[stopping].";
	     rule succeeds.

Test me with "take omega / omega, mail / turn on omega / omega, mail / omega, calendar / g / g / omega, sing / mail".
```
