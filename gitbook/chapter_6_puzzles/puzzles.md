# Chapter 6: Puzzles

![](../assets/graphics8.png)

In the short section on puzzles in Chapter 1, I pointed out that a few games are “puzzleless,” but that most games have a few puzzles, or a lot of them. The point of including puzzles is that the player becomes a sort of collaborator in the unfolding of the story. The story will only move forward when the player takes some action.

Almost any sort of action might be required — watering a tiny plant, for instance, might turn it into a giant beanstalk that can be climbed. But possibly the most basic form of puzzle in IF is the locked door. The player doesn’t yet have the key that unlocks the door, and has to hunt for the key. Unlocking and opening the door will give the player access to a new room, or perhaps to an entirely new region of the model world containing dozens of rooms.

The way I look at it, every puzzle in every game, no matter what form it might take, is ultimately not very different from a locked door. You can’t see what’s on the other side until you find the key, whatever the key is. What’s on the other side might be a physical location or a series of new events. The “key” might be an apple that you need to give to the wicked witch so she’ll go to sleep so you can rescue the children in the oven. In some sense, the apple is a key, although the code you’ll write to handle the command GIVE APPLE TO WITCH will probably look somewhat different from the code for UNLOCK DOOR WITH KEY.

In this chapter we’ll take a look at many of the common types of puzzles, and suggest a few ways to implement them. This is not, I hasten to add, a complete inventory of puzzle types. It’s intended merely to introduce a few ideas that new IF writers may not have considered.

IF authors have written lots of essays and tips about puzzles. Stephen Granade has a good short essay, for instance, on his Brass Lantern website (http://brasslantern.org/writers/iftheory/betterpuzzles-a.html). Graham Nelson’s manual on programming Inform 6, the _Designer Manual 4_ (usually called the DM4),has a very good section on designing puzzles; currently this is to be found at http://inform-fiction.org/manual/DM4.pdf. (In case you’re unfamiliar with Inform 6, perhaps I should add that nothing else in the DM4 will be of much use to you as an Inform 7 author — at least not until you start writing I6 inclusions, an advanced type of programming not covered in this _Handbook._)

I like to include some easy puzzles in a game, and a few hard ones. But as a player, I prefer the easy ones, because I’m very bad at puzzle-solving. While playing other people’s games, I often get stuck. Many authors feel that it’s a good idea to help players by including some form of hint system in the game. You’ll find some advice on how to set up a hint system in Chapter 10. Other authors feel that providing hints spoils the game, or is just too much trouble.
