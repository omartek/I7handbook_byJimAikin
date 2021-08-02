## Overview

To begin with, your players will probably want to be able to talk to the other characters. There are several ways to set up a conversation system. Each method has advantages, and also weaknesses, as we’ll see.

One common reason to want to have a conversation with a character is to try to learn something useful. If you’re writing a game about criminals, for instance, ASK POLICEMAN ABOUT BURGLAR might be an important command for the player to try. Another reason to have a conversation is because you hope to cause the character to do something. If the player types TELL POLICEMAN ABOUT BURGLAR, the policeman might rush off to arrest the burglar — a real change in the world of the story that won’t take place unless the player gives that command.

The player character may need help doing something, and may want to ask another character for help. For instance, a player character who has only normal strength might want to enlist the aid of a weight-lifter to move a boulder. So the player may need a way to give instructions to other characters. ASK REGINALD TO LIFT THE BOULDER could be an important part of the game.

Characters may have possessions that the player needs. One common type of instruction is to ask for an object. If you ASK MARY FOR DIAMOND NECKLACE, she might refuse to part with it, or she might give it to you, depending on how the game is written.

Some characters are stationary — they’re always in one room. Other characters may wander around the map. They may follow the PC, or run away when the PC approaches.

Characters will sometimes carry out simple tasks on their own, such as stealing things from the player or even killing the player.

When a character is in the same room as the player, the character may seem more lifelike if it’s carrying out some sort of “stage business,” engaging in a minor activity every turn, or once every few turns, just to remind the player that there’s someone else in the room. If the character is doing this type of stage business, nothing is likely to change in the room (although it could — the butler might be polishing the silverware for 20 turns, and at the end of that time the description of the silverware might change to say that it’s spotless and shining). All that usually happens is that the game prints out a brief message describing a nonexistent action.

If your story takes place in a world where there’s lots of fighting (swordfights or laser guns, your choice!), you may want the player to engage in hand-to-hand combat with other characters.

Groups of characters require special handling. If your player character is facing a crowd of angry villagers armed with torches and pitchforks, you probably don’t want to create a hundred different villager characters. For one thing, it’s a lot of work, and you won’t gain much in terms of realism or a more dramatic story. A better method will usually be to create a single “crowd” object (which might not be a person at all, as far as Inform is concerned) and then create a single “spokesperson” man or woman, an actual Inform NPC object, who will engage in any conversation or other activities. On the other hand, if you’re writing an Agatha Christie type of murder mystery, you may want to have as many as six or seven individual characters (the suspects) all sitting around in the drawing room at the same time. Inform provides some fascinating tools with which to allow these characters to relate to one another. (See the discussion of relations in Chapter 9 of this _Handbook,_ [here](../chapter_10_advanced_topics/relations.md#relations)) **[Check reference.]**
