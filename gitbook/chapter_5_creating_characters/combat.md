## Combat

I’ve never used the extension called Armed by David Ratliff, but a couple of my students have found it useful. The version on the Inform 7 website doesn’t work with current versions of Inform, as it was written in 2008\. Fixing it is not terribly difficult. The phrase “end the game” has to be changed to “end the story”, instances of “change … to” have to be changed to “now … is”, and you may want to fix a misspelled word or two. The biggest stumbling block is that one of the Check rules in Armed, called the can’t take it with you rule, uses the word “ignore”. This feature is no longer supported. I was able to work around the problem by replacing that rule with this new code:

```ìnform7
Check an actor taking (this is the new can't take people's possessions rule):
        let the local ceiling be the common ancestor of the actor with the noun;
        let the owner be the not-counting-parts holder of the noun;
        while the owner is not nothing and the owner is not the local ceiling:
                if the owner is a person and the owner is not dead:
                        if the actor is the player:
                                say "[regarding the noun][Those] [seem] to belong to [the owner]." (A);
                        stop the action;
                let the owner be the not-counting-parts holder of the owner;

The new can't take people's possessions rule is listed instead of the can't take people's possessions rule in the check taking rulebook.
```

In case you’re curious, I created this code by copying the original can’t take people’s possessions rule in Standard Rules and adding the words “and the owner is not dead” to line 5.

Armed creates several kinds of weapons, allows you to set the maximum amount of damage that will be inflicted by a weapon, and computes the health of each character based on the amount of damage they’ve suffered. If you only want to add some weapons to your game, it might be easier to do it yourself, because Armed prints out the health of each character when the character is examined, and the health of the player character when the player takes inventory. If most of your game doesn’t involve combat, the printout of characters’ health is likely to be a bit distracting.

If all you need to do is set up one encounter in which some combat takes place, here’s some code that will get you started. Note that we need to create an action called “attacking it with”. Inform’s standard library includes attacking, but not attacking it with. In the code below, we’ve set it up so that if the player tries ATTACK THE DUKE without naming a weapon, we don’t get Inform’s default response, “Violence isn’t the answer to this one.” Since violence _is_ the answer to this one, it’s important not to confuse the player.

```ìnform7
The Drawbridge is a room. "Fortunately for you, brave knight, the drawbridge has not been raised. The castle lies before you to the east."

The Castle is east of the Drawbridge.

The Duke is a man in the Drawbridge. "The evil duke stands before you, blocking your way menacingly with a rapier." The description of the duke is "He has an evil glint in his eye."

Instead of going east from the drawbridge when the Duke is in the Drawbridge:
        say "'You shall not pass!' cries the duke."

The player carries a sword and a sofa cushion.

The Duke’s dead body is a thing.

Check attacking the duke:
        say "With your bare fists? Surely you can think of a better way!" instead.

Attacking it with is an action applying to two things and requiring light. Understand "attack [something] with [something]" and "hit [something] with [something]" as attacking it with.

Check attacking it with:
        if the second noun is the sofa cushion:
                say "'Do not mock me thus, vile varlet!' shouts the duke." instead;
        else if the second noun is not carried by the player:
                say "You're not holding [the second noun]." instead.

Report attacking it with:
        say "Your aggressive action has no visible result."

Instead of attacking the duke with the sword:
        if a random chance of 1 in 3 succeeds:
                say "You hack the duke to pieces with the sword!";
                remove the duke from play;
                now the duke’s dead body is in the location;
        otherwise:
                say "The duke parries your clumsy thrust expertly with his rapier."
```

We’re using randomness in the Instead rule above to allow the attack to succeed sometimes and fail other times. In a real game, you might want to include a small chance that the duke will kill the player. Since we may want to do any of three things in our Instead rule, we can’t use the “if a random chance … succeeds” syntax, since that only allows for a positive or negative result. Instead, we’ll do it by creating a temporary variable, X, and assigning it a random value. Replace the Instead rule above with this one:

```ìnform7
Instead of attacking the duke with the sword:
        let X be a random number from 1 to 5;
        if X is 1:
                say "You hack the duke to pieces with the sword!";
                remove the duke from play;
                now the duke’s dead body is in the location;
        otherwise if X is 2:
                say "The point of the duke's rapier enters your rib cage.";
        end the game in death;
        otherwise:
                say "The duke parries your clumsy thrust expertly with his rapier."
```
