## Conversations, Part IV: Menu-Based Conversation

In a menu-based conversation, the player who starts talking with an NPC is presented with a menu of options, and selects one of the responses by number. The output might look something like this:

```
>talk to madelyn
You could:
[1] compliment Madelyn on her hair.
[2] complain that the gunfire in the street kept you awake all night.
[3] ask Madelyn why Uncle Jack was sent to prison.
[4] say goodbye.

>1
“You have really lovely hair,” you tell Madelyn.

“Do you like it?” she replies, patting a stray strand into place. “I’m not sure avocado green is really a good color on me.”
```

By typing a “1” at the prompt, the player selects the first item in the conversation menu. What usually happens is that after the output of item 1 is printed, the menu comes back again, but now with item 1 removed. Eventually, there will be nothing left in the menu except “say goodbye.” The player will select that item, read the output, and the conversation is finished.

One advantage of this type of conversation system is that it can read in a more realistic way than bare commands like TELL MADELYN ABOUT HAIR and ASK MADELYN ABOUT UNCLE JACK. Another advantage is that the player is automatically directed toward topics of conversation that may be interesting or important to the story. But there are two problems. First, setting up this type of conversation system is not quite as easy as creating an ask/tell system. Second, the player will most likely just go through all of the possible topics one by one to see what they say. This process is called “the lawnmower effect,” because it turns the game-play into a rather boring mechanical process of mowing down everything on the menu.

If you look on **p. 7.8** of the _Recipe Book_, “Saying Complicated Things,” you’ll find several examples of conversational systems. Example 282, “Sweeney,” provides a hybrid system in which the player can ask or tell about topics, but will sometimes be prompted with a numbered list of items. The Recipe Book doesn’t give an example of a full menu-based conversation system, reporting that “they can be long-winded to set up, and therefore none are exemplified here, but several have been released as extensions for Inform.”

Unfortunately, the Extensions that do this seem to be very obsolete. I tried updating Quip-Based Conversation by Michael Martin, but was unable to get it to compile.
