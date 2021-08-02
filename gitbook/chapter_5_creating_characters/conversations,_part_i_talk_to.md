## Conversations, Part I: talk to

![](../assets/graphics13.jpg)

The easiest way to let your players talk to NPCs is by creating a “talk to” action. Here’s a code sample that will produce a simple conversation:

```inform7
Talking to is an action applying to one visible thing. Understand "talk to [someone]" or “converse with [someone]” as talking to.

Check talking to: say "[The noun] doesn't reply."

Instead of talking to Troy:
        say "[one of]'Hi, there,' you say confidently.[paragraph break]'What's happening?' he replies casually.[or]'I've been meaning to ask you about that tuxedo,' you comment. 'Where did you get it?'[paragraph break]'My tailor is quite exclusive,' Troy replies, inspecting his cuff. 'He would never consent to clothe riffraff like you.'[or]'You really are a stuck-up snob, aren't you?' you say hotly.[paragraph break]Troy laughs heartily. 'I was just yanking your chain. I bought it at Macy's for $60 at a clearance sale. I'll give it to you if you like.'[or]You decide against talking any further with Troy right now.[stopping]".
```

The most interesting thing about this code is what happens in the long “say” block. This is set up to give Inform some alternative outputs. The structure looks like this: “[one of]...[or]...[or]...[or]...[stopping]”. This structure is covered down near the bottom of **p. 5\. 7** of _Writing with Inform_, “Text with random alternatives”; also see Chapter 8 of the _Handbook,_ [here](../chapter_9_phrasing_&_punctuation/text_insertions.md#text-insertions).

When you use this type of code, the player can type TALK TO TROY, read the first response (up to “[or]”), then type AGAIN (or just G) to read the second response, and so on. The last response (the one just before “[stopping]” should always be used to indicate to the player that there’s nothing further to be gained by trying to talk to the character. Note also the use of “[paragraph break]” for the outputs that are separated into paragraphs. The output will look like this:

```
>talk to troy
"Hi, there," you say confidently.

"What's happening?" he replies casually.

>g
"I've been meaning to ask you about that tuxedo," you comment. "Where did you get it?"

"My tailor is quite exclusive," Troy replies, inspecting his cuff. "He would never consent to clothe riffraff like you."

>g
"You really are a stuck-up snob, aren't you?" you say hotly.

Troy laughs heartily. "I was just yanking your chain. I bought it at Macy's for $60 at a clearance sale. I'll give it to you if you like."

>g
You decide against talking any further with Troy right now.
```
The good thing about a talk to conversation system is that it’s easy to set up. The bad thing is that it’s quite limited. If the player wants to ask or tell the character about three or four different things that may be significant to the story, a talk to system may not do the job. It’s possible to set up a TALK TO system with logic tests in the Instead rule — tests such as “if the cellar has not been visited” could produce two different streams of conversation depending on whether the cellar has been visited. But if the conversation is going to move the story forward, it’s up to the player to use the AGAIN command several times in order to make sure the conversation is finished, and then perhaps start a new conversation later.

Another problem is that if the player should try TALK TO TROY only twice, go to a different room, return a hundred turns later, and try TALK TO TROY again, the conversation will continue as if there had been no interruption. This is not realistic.

One easy way to make TALK TO work more flexibly uses Inform’s scenes feature (see Chapter 7 of the _Handbook_):

```inform7
Instead of talking to Troy during Cocktail Hour:
```

A different but also handy use for the TALK TO command might be to have your game print out some suggested topics for conversation. This use of the TALK TO command doesn’t produce any actual conversation; the conversation would occur in an ASK ABOUT or TELL ABOUT command, which is the subject of the next section.

```
>talk to bishop
```

You could ask the bishop about the crypt, about the impending eclipse, or about the Uzi he’s carrying.

This list of possible topics can be fixed, or you can write some code that will put it together while the game is being played. After the player has asked about the crypt, for instance, this topic might disappear from the list of suggested topics, that topic being exhausted. An extension called Conversation Suggestions by Eric Eve will give you a framework for setting up topic suggestion lists of this sort. (Note that Conversation Suggestions is not compatible with the simple TALK TO code suggested above.)
