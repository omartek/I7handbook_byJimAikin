## Same Action, New Results

Some puzzles are designed to force the player to take a given action several times. For instance, the player might be required to knock on a door three times before someone will open the door. To do this in Inform, you would most likely use Instead rules and the phrases “for the first time,” “for the second time,” “for the third time,” and so on. It’s important also to write a default rule for handling the action if it’s attempted more often than you’ve explicitly allowed for. In the example below, the Report rule for our new knocking on action takes care of this.

```inform7
The chapel door is west of the Grand Entry Hall and east of the Chapel. The chapel door is a door. The chapel door is scenery and locked.

Knocking on is an action applying to one thing and requiring light. Understand "knock on [something]" and "tap on [something]" as knocking on.

Check knocking on:
        if the noun is the player:
                say "Your head makes a hollow sound." instead;
        otherwise if the noun is a person:
                say "That wouldn't be polite." instead.

Report knocking on:
        say "You tap gently on [the noun], but nothing happens."

Instead of knocking on the chapel door for the first time:
        say "The sound of your knuckles generates booming echoes within the chapel. For a moment you think you hear someone moving around inside, but the door remains closed."

Instead of knocking on the chapel door for the second time:
        say "Within the chapel, a faint and uncertain voice cries, 'I'm coming, I'm coming.' You wait patiently for a minute, but the door doesn't open."

Instead of knocking on the chapel door for the third time:
        now the chapel door is open;
        say "After a few more interminable minutes of waiting, the door swings ponderously open. A man in a clerical collar, who looks to be at least a hundred years old, peers out at you through rheumy eyes. 'I'm sorry,' he says. 'We're no longer admitting worshippers. God is dead, you see.'"
```

If you write a puzzle like this, it’s important to give the player a clue that the action should be repeated. If the first response to KNOCK ON DOOR is a bare “Nothing happens” or some similar phrase, the player is unlikely to try the action again.
