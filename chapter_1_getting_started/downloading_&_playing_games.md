## Downloading &amp; Playing Games {#downloading-playing-games}

One of the best ways to learn about game design is to download and play a few games. A good place to start looking for games is the Interactive Fiction Database (https://ifdb.org/). On this site you can read reviews of games, search for games by a particular author, and click links to download the games themselves. Some games on this site can be played online, in your browser, without downloading.

Other resources for finding games include Baf’s Guide (https://www.wurb.com/), though that site seems to be defunct at the moment, and an online magazine called SPAG (the Society for the Promotion of Adventure Games, https://www.sparkynet.com/spag/). SPAG is currently inactive, but the site is still up. Some games are available from authors’ websites, but far more are to be found in the Interactive Fiction Archive (https://www.ifarchive.org/). You can find many Inform games in the games/glulx directory of the Archive.

To play text games, you’ll generally need both the game file itself and a separate piece of software called an **interpreter**. After downloading and installing an interpreter, you’ll load the game into the interpreter to play it. A few games written in TADS and some other development systems are available as free-standing programs for Windows. Inform games in the .z5 and .z8 formats can be played in a Web browser using the Parchment system (http://parchment.toolness.com/). A browser-based game player for large Inform games in the Glulx format is called Quixe. At this writing Quixe is close to being complete, which is good news indeed for Inform authors.

Currently the best interpreter is called **Gargoyle**. It’s available for both Windows, Mac & Linux. To find it, go to http://ccxvii.net/gargoyle. Gargoyle can play all Z-code (Inform) and Glulx games, as well as TADS games and Hugo games.

### What’s This .z8 Stuff All About, Anyway? {#what-s-this-z8-stuff-all-about-anyway}

![](../assets/graphics20.jpg)

In the beginning, there was Zork. Well, no, that wasn’t quite the beginning. In the beginning was Adventure. Adventure was the very first text-based computer game. It was freely copied and shared by computer users in the 1970s, and was never a commercial product. But around 1980, some clever people saw that they could make money on text-based games. They started a company called Infocom. The first game that came from Infocom was called Zork.

Zork was enormously successful, and led to a series of sequels, which were also successful. But then, in the mid-1980s, computers became fast enough to display graphics. Games that used graphics were much sexier than text games. As a type of commercial product, text games pretty much died. (Not entirely. Here and there you might find a text game for sale — for example, at this writing Andrew Plotkin’s “Hadean Lands” is available for iOS through the App Store. Text games are no longer a big business, though.)

By the late 1980s, the text game boom had passed, but there were still hundreds of thousands of computer users who owned Zork or one of Infocom’s other games. These games were available for many different computer operating systems (and at the time, there were a lot more computer operating systems than there are today). The actual game data was the same no matter what type of computer you owned, but Infocom created a _virtual machine_ for each operating system. A virtual machine ... well, let’s not worry about the technical details. A virtual machine is a piece of software that pretends to be a piece of hardware. The point is, if you had a virtual machine from Infocom for your computer, you could play any of Infocom’s games. All you needed was the data file for a particular game. You loaded the data file into the virtual machine, and the game would appear on your screen.

The virtual machine developed by Infocom is what came to be called the Z-machine. (Named after Zork, you see.) Even after Infocom closed its doors, the Z-machine was still widely available, because a lot of people had copies, and in those days copy-protected software was still a few years in the future.

So when Graham Nelson started working on the first version of Inform in the early 1990s, he made a very smart decision: He wouldn’t try to write his own game delivery system from scratch. Instead, he’d create an IF programming language that would produce game files that could be loaded into the Z-machine. Inform was written in such a way that its compiler would create Z-machine-compatible game files. These could then be played by anyone who had a Z-machine on a disk. This was one of several factors that insured the success of Inform.

Computers in those days had very little memory compared to computers today, so the Z-machine had to be small and efficient. It could load and run several different file types, but the most common had names that ended with .z5 and .z8\. A .z5 file could be as large as 256Kb (yes, that’s kilobytes, not megabytes), while the larger .z8 format could be used for games that needed to be as large as 512Kb.

Today, the Infocom-era Z-machine is ancient history. If you still have an Atari or Kaypro computer in working condition, and a Z-machine interpreter for that computer, you could play a game written today in Inform, as long as the game was compiled as a .z5 or .z8 file. But who owns a Kaypro anymore? Today, several newer IF interpreters have been written that are compatible with the original Z-machine game file format. These have names like Frotz and Nitfol (both of which were magic words in one of the Zork sequels).

In order to allow Inform authors to write larger games, Andrew Plotkin created the Glulx game format. Glulx games can be much larger, and can include sounds, graphics, and multiple sub-windows within the main game window. Glulx games can be played on any modern personal computer, since Glulx interpreters exist for Macintosh, Windows, and Linux. However, Glulx games are mostly too large to play on cell phones and other hand-held devices. Z-machine interpreters are available for some popular hand-helds. (Frotz is available for the iPhone, for instance.)