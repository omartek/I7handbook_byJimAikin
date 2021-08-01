## Giving Orders to Characters {#giving-orders-to-characters}

The standard command that players can use to give orders to NPCs is in the form BOB, EAT THE PANCAKE. The NPC’s name is what grammarians call a “noun of address,” and is followed by a comma. If you want your game to respond to the alternate forms ASK BOB TO EAT THE PANCAKE and TELL BOB TO EAT THE PANCAKE, one easy way to do it is with an “after reading a command” rule. This type of rule intercepts the player’s input before it reaches the parser. You can change the player’s input in whatever way you like. This could be a sneaky way of creating an infuriatingly difficult puzzle, but here we’ll use it in a more friendly way:

```inform7
After reading a command:
        let T be text;
        let T be the player's command;
        replace the regular expression "tell bob to" in T with "bob,";
        replace the regular expression "ask bob to" in T with "bob,";
        change the text of the player's command to T.
```

The main thing to be aware of here is that if your NPC can be referred to as “Bob”, “Uncle Bob”, “Uncle”, or “man”, the After Reading a Command rule needs to process _all_ of those possible inputs separately, because the parser hasn’t yet had a chance to figure out what object the player’s command is referring to. The words “man” and “woman” will be especially sticky, because you might have several different NPCs in your game that can be referred to as “man” or “woman”.

Inform won’t let you rewrite the rule so that it reads “After reading a command in the presence of Bob”. But you can do it this way:

```inform7
After reading a command:
        let T be text;
        let T be the player's command;
        if Bob is in the location:
                replace the regular expression "tell bob to" in T with "bob,";
                replace the regular expression "ask bob to" in T with "bob,";
                replace the regular expression "tell man to" in T with "man,";
                [...and so on for any other words that can refer to Bob...]
        change the text of the player's command to T.
```

Now the player can give orders to an NPC using a variety of normal phrases. But there’s a better way, which was suggested by Emily Short. This uses Inform’s ability to match regular expressions — frankly not a topic that belongs in a handbook for new authors. (If you’re curious, have a look at **p. 20.6** in _Writing with Inform_, “Regular expression matching.”) The code below will handle giving orders to all of the characters in your game:

```inform7
After reading a command:
        let N be text;
        let N be the player's command;
        replace the regular expression "\b(ask|tell|order) (.+?) to (.+)" in N with "\2, \3";
        change the text of the player's command to N.
```

But by default, NPCs will refuse to follow orders. If you want an NPC to obey the player, you need to write a **persuasion rule**, as explained on **p. 12.4** of _Writing with Inform_, “Persuasion.” A persuasion rule can be as specific or as broad as you like — you can have all NPCs obey orders, or only have one NPC obey one specific order. Here’s how to do it with two specific actions. We’re going to allow Uncle Jack to take the jewels or give them to the player:

```inform7
Persuasion rule for asking Uncle Jack to try taking the jewels:
        persuasion succeeds.
Persuasion rule for asking Uncle Jack to try giving the jewels to the player:
        persuasion succeeds.

Instead of Uncle Jack giving the jewels to the player:
        now the player carries the jewels;
        say "Jack hands you the jewels.";
        rule succeeds.
```

This code assumes that the jewels are in scope. (Perhaps Uncle Jack is already carrying them.) If you need an NPC to give the player something that has only been talked about, but that isn’t in the room at the moment, you have a slightly more complex problem. The easy way to deal with this is to have the NPC carry the object, but make it a concealed possession, as explained on **p. 3.24** of _Writing with Inform_ (“Concealment”):

```inform7
Troy is a man in the Billiard Room. Troy carries a banana.

Rule for deciding the concealed possessions of Troy: if the particular possession is the banana, yes; otherwise no.

Persuasion rule for asking Troy to try giving the banana to the player:
        persuasion succeeds.

Instead of Troy giving the banana to the player:
        say "Troy gives you the banana.";
        now the player carries the banana;
        rule succeeds.
```

When the banana is concealed, the player won’t be able to X BANANA, but the banana will still be in scope, so TROY, GIVE ME THE BANANA will work as expected.
