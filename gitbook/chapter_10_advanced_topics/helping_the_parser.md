## Helping the Parser

Sometimes a word in your game will be ambiguous — that is, the parser will be able to interpret it in two or three different ways. When possible, you should use unique words to refer to every object in your game, but sometimes that’s just not possible.

A handy trick for helping the parser deal with this type of ambiguity is to write a Does The Player Mean rule. The way to do this is explained on **p. 17.19** of _Writing with Inform_, “Does the player mean....” Other useful techniques are shown on **pages 17.17** (“Context: understanding when”), **17.20** (“Understanding mistakes”),and **17.21** (“Precedence”). One of my favorite techniques (from 17.17) is writing Understand When rules. We’ve seen a couple of these elsewhere in the _Handbook_. Such a rule might look like this:

```inform7
Understand "cracked" and "chipped" as the Ming vase when the Ming vase is broken.
```

When you put this rule in your code, the words “cracked” and “chipped” will not be understood as referring to the vase if the vase is not broken. Writing conditions that refer to specific scenes is also useful:

```inform7
Understand "dismantled" as the robot when Emergency Repairs is happening.
```

### Pronouns {#pronouns}

Inform’s parser tries to make intelligent guesses about what the player means when she uses words like “it”, “them”, and “him” in commands. But occasionally this mechanism will go astray. In a few cases, such a lapse can seriously confuse the player. Consider this transcript:

```
>put bullet in revolver
You put the bullet into the revolver.

>point it at dave
Nothing happens.

>point revolver at dave
Dave backs away from you, saying, "No! No!"
```

In this case, the player understands that “it” is the revolver, but the parser thinks “it” is the bullet. If the player only uses the command containing “it”, she will conclude (erroneously) that Dave is not intimidated by the loaded revolver. To solve this problem, you can use the phrase “set pronouns from” in your code:

```inform7
After inserting the bullet into the revolver:
        set pronouns from the revolver;
        continue the action.
```
