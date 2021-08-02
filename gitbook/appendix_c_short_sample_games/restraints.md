## Restraints

Preventing the player from performing certain actions in certain situations is a standard type of puzzle. For instance, if the player is wearing handcuffs, picking things up (that is, using the TAKE or GET command) probably shouldn’t work. I’ll leave it up to your imagination to figure out how the player character might be able to remove a pair of handcuffs while unable to pick up the key. In the example below, a simple workaround is used — the player is allowed to pick up the key, but nothing else.

This example, which was posted by Zeborah on the forum at intfiction.org and then revised by me with a little help from Mike Tarbert, provides a general-purpose way to intercept actions depending on what sort of restraint the PC is wearing. It uses a table to correlate actions with restraints.

```inform7
A restraint is a kind of thing. A restraint is usually wearable. The blindfold, the gag, the ball-and-chain, and some handcuffs are restraints.

Instead of doing something when the player wears a restraint:
      	repeat through the Table of Restricted Movements:
            		if the player wears the restraint entry:
                  			let impulses be a list of action names;
                  			let impulses be the movement entry;
                  			if the action name part of the current action is listed in impulses:
                        				say "You have no hope of [the current action] while wearing [the restraint entry]." instead;
      	continue the action.

The handcuffs can be locked or unlocked. The handcuffs are locked.

Instead of locking the handcuffs with the small iron key:
      	if the handcuffs are locked:
            		say "They're already locked.";
      	otherwise if the player does not carry the small iron key:
            		say "You don't seem to have the key.";
      	otherwise:
            		now the handcuffs are locked;
            		say "You lock the handcuffs with the small iron key."

Instead of taking off the handcuffs:
      	if the handcuffs are locked:
            		say "The handcuffs seem to be locked.";
      	otherwise:
            		now the player carries the handcuffs;
            		say "You remove the handcuffs."

Instead of wearing the handcuffs:
      	if the handcuffs are worn:
            		say "You're already wearing the handcuffs.";
      	otherwise if the handcuffs are locked:
            		say "You'll need to unlock the handcuffs before you can put them on.";
      	otherwise:
            		now the player wears the handcuffs;
            		say "You put on the handcuffs."

Instead of unlocking the handcuffs with the small iron key:
      	if the handcuffs are unlocked:
            		say "But they're not locked!";
      	otherwise if the player does not carry the small iron key:
            		say "You don't seem to have the key.";
      	otherwise:
            		now the handcuffs are unlocked;
            		say "It's awkward, but you manage to insert the key in the keyhole and turn it. Now the handcuffs are unlocked."

Instead of taking the small iron key when the player wears the handcuffs:
      	now the player carries the small iron key;
      	say "You manage to pick up the key, even though you're wearing handcuffs."

Instead of opening the tool chest when the player wears the handcuffs:
      	if the tool chest is open:
            		say "It's already open.";
      	otherwise:
            		now the tool chest is open;
            		say "It's awkward, but you manage to open the tool chest while wearing the handcuffs."

The Dungeon is a room. "A dank and dismal dungeon. You can go north."

The Dismal Crypt is north of the Dungeon. "The walls of the crypt are oozing...."

The player wears the ball-and-chain and the handcuffs.

The tool chest is an openable container in the Dungeon. The tool chest is closed. The blindfold and gag are in the tool chest. The small iron key is in the tool chest.

[Due to a bug in the Inform compiler, we have to split the list of actions that you can’t take while wearing the handcuffs into three separate rows in the table:]

Table of Restricted Movements
restraint	      movement
ball-and-chain	{going action, jumping action, entering action, exiting action, getting off action, climbing action}
gag	{eating action, kissing action, answering it that action, telling it about action, asking it about action, asking it for action, saying yes action, saying no action, tasting action, saying sorry action}
handcuffs	{taking action, removing it from action, taking off action, dropping action, putting it on action, inserting it into action, searching action, touching action}
handcuffs	{waving action, pulling action, pushing action, turning action, squeezing action, eating action, consulting it about action, locking it with action, unlocking it with action, switching on action, switching off action}
handcuffs	{opening action, closing action, wearing action, attacking action, showing it to action, throwing it at action, cutting action, tying it to action, drinking action, swinging action, rubbing action, setting it to action}
blindfold	{looking action, searching action, examining action}

Test me with "n / remove ball-and-chain / remove handcuffs / open chest / unlock handcuffs with key / remove handcuffs / remove ball-and-chain / n".
```

This example takes advantage of the fact that when the Inform compiler builds rulebooks, it lists more specific rules ahead of more general rules. The Instead rules for the tool chest, key, and handcuffs will be listed before the general-purpose Instead rule, so they’ll allow the player to solve the puzzle by opening the chest, picking up the key, and then unlocking the handcuffs.

The example also shows how to use a table containing list entries, and how to use the phrase “action-name part of the current action,” which is not a syntax mentioned elsewhere in this _Handbook_ (nor, for that matter, in _Writing with Inform_). It’s a useful syntax to know. For instance, if the current action is “going north”, the action-name part of the action is “going”.

After removing the handcuffs, you can experiment further with this example by wearing the blindfold and trying to examine things, or by adding an NPC, wearing the gag, and then trying to talk to the NPC.
