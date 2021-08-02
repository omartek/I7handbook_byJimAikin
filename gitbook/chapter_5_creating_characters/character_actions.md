## Character Actions

A good way to make a character seem more alive is for the character to react in some way when the player does something. This reaction could range from a simple comment to an explosive act.

Let’s suppose that old Alexander Button seems to be asleep in his chair. But he isn’t asleep, really. If you pick up the piece of paper on the table, he’ll snatch it away from you:

```ìnform7
Alexander Button is a man in the Living Room. "Old Alexander [if Alexander carries the will]eyes you keenly[otherwise]seems to be asleep[end if]." The description is "He must be at least 90[if Alexander carries the will]. He's wide awake, and looking at you in a doubtful way[otherwise]. He seems to be asleep[end if]."

The end table is a scenery supporter in the Living Room.

The will is on the end table. The description is "A legal-looking piece of paper. You can't read what's on it, because it's upside down."

After taking the will:
        now Alexander carries the will;
        say "Alexander's eyes fly open. 'So ... snooping, eh?' He snatches the will away from you."
```

To get Alexander to react, we use an After rule. An After rule is a good idea here, because it allows Inform to do its usual processing of the TAKE PAPER command. Only if the command succeeds — if it’s possible for the player to take the will — will Alexander react.

The NPC action above was triggered by a taking action. Sometimes, we may want a character to react to something he or she sees. For instance, the character might demand that the player give him an object the player is carrying. Here’s a short game that shows how this might work:

The Dusty Street is a room. "The unpaved street of Tombstone, Arizona, runs east and west here. The Red Dog Saloon is to the north."

The Red Dog Saloon is north of the Dusty Street. "The sour smell of spilled whiskey permeates this rough-hewn room, which is dim after the sunlit glare of the street."

Sheriff Earp is a man in the Red Dog Saloon. "Wyatt Earp is standing at the bar." Understand "Wyatt" as Sheriff Earp. The description is "Earp looks lean and mean. He's wearing a badge."

The player carries a six-gun. Understand "gun" and "revolver" as the six-gun.

Every turn:
        if the player carries the six-gun and Sheriff Earp can see the six-gun:
                say "[one of]'I see you're packin['] a weapon,' the sheriff says. 'Packin['] a weapon in town is illegal. Best you hand it over.'[or]'Well, are you gonna give me that six-gun, or ain't you?' Earp stares at you meaningfully.[stopping]".

Instead of going in the Red Dog Saloon:
        if the player carries the six-gun and Sheriff Earp can see the six-gun:
                say "'Best you not be walkin['] out of here with that firearm,' Earp says. He adjusts his own gunbelt slightly, as if he's thinking he may have to draw down on you.";
        otherwise:
                continue the action.

Instead of giving the six-gun to Sheriff Earp:
        now Sheriff Earp carries the six-gun;
        say "You hand over the gun. 'Thanks,' Earp says. 'You can go now. But don't be startin' any trouble, you hear?'"

Test me with "i/ n / s / give gun to Earp / s / i".
```

In this example, the work is being done by the Every Turn rule and the Instead Of Going rule. The player can do anything in the saloon (in a real game, this might include ordering a drink or sitting down to play poker, actions that would likely cause the sheriff to become more and more insistent), but can’t leave until he has given the gun to the sheriff.
