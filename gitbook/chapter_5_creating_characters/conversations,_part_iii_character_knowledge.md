## Conversations, Part III: Character Knowledge

During the course of a game, an NPC might learn something, and what the NPC knows might change how he or she responds during a conversation. For instance, let’s suppose the PC has witnessed Aunt Mary’s house burning down, and is now in conversation (in a different location) with Uncle Jack. Uncle Jack won’t know about the fire until the player tells him — so the command ASK JACK ABOUT MARY might need two different outputs, depending on whether or not Uncle Jack knows that Aunt Mary is now without a home.

The extension called Epistemology by Eric Eve won’t take care of this for us, because it’s intended to track what the PC knows, not what an NPC knows. In this example, though, we’re going to use Conversation Responses by Eric Eve. Conversation Responses includes Epistemology, which is convenient for this example, because the player can’t ASK JACK ABOUT MARY unless the player has previously seen or is familiar with the Aunt Mary object. Both the “seen” and “familiar” properties are defined in Epistemology.

```inform7
Include Conversation Responses by Eric Eve.

Aunt Mary is a woman. Aunt Mary is familiar.

The fire is a thing. The fire is familiar. Understand "blaze" and "conflagration" as the fire.

The Living Room is a room.

Uncle Jack is a man in the Living Room.

Jack-knows-about-fire is a truth state that varies. Jack-knows-about-fire is false.

Response of Jack when asked about the fire:
        if Jack-knows-about-fire is false:
                say "'Have you heard about the fire?' you ask.[paragraph break]'My goodness, no!' he replies. 'Tell me about it!'";
        otherwise:
                say "'I only know what you told me,' he says."

Response of Jack when told about the fire:
        if Jack-knows-about-fire is false:
                say "'I saw Aunt Mary's house burn down,' you tell Uncle Jack.[paragraph break]'Oh, no!' he cries. 'All those lovely antiques, burnt to a crisp!'";
                now Jack-knows-about-fire is true;
        otherwise:
                say "'I already told you about the fire, didn't I?' you say.[paragraph break]'Yes, yes,' Uncle Jack says, shaking his head sadly."

Response of Jack when asked-or-told about Mary:
        if Jack-knows-about-fire is true:
                say "'What do you suppose will happen to Aunt Mary now?' you ask.[paragraph break]'I guess she'll have to move in with her daughter,' Uncle Jack replies.";
        otherwise:
                say "'Isn't it too bad about Aunt Mary?' you comment.[paragraph break]'My goodness,' Jack exclaims. 'Did something happen?'[paragraph break]'Yes, her house burnt down,' you tell him.";
                now Jack-knows-about-fire is true.
```

In this example I’ve created Jack-knows-about-fire as a truth state that varies. In a game where the software needs to keep track of an NPC’s knowledge on a variety of subjects, keeping the data in a table (see [here](../chapter_10_advanced_topics/tables.md#tables)) might be easier.

If you study this code for a minute, the way it works should become clear. The player can ask or tell Jack about the fire. The player can either ask or tell Jack about Mary. These conversations test whether Jack-knows-about-fire is true. If it’s false, Jack’s response is different. If the player tries asking Jack about the fire before Jack knows about it, Jack will ask for more information.
