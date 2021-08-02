## I6 Constants {#i6-constants}

As your game is compiled, Inform goes through two processes. First, your source text and all of the extensions you’re using (plus the Standard Rules) are turned into Inform 6 (I6) code. The I6 compiler then runs, producing a playable .z8 or glulx game, depending on which format you have chosen in the Settings tab. Occasionally, the compilation process will stop at the second stage. This can happen for several reasons, but one of the more common and less troublesome reasons is because you’re using too much of something, and I6 thinks it’s running out of room.

The Standard Rules define a series of constants, each of which controls the amount of memory available in the game for a certain type of data. Here’s the list:

```inform7
Use ALLOC_CHUNK_SIZE of 32000.
Use MAX_ARRAYS of 10000.
Use MAX_CLASSES of 200.
Use MAX_VERBS of 255.
Use MAX_LABELS of 10000.
Use MAX_ZCODE_SIZE of 500000.
Use MAX_STATIC_DATA of 180000.
Use MAX_PROP_TABLE_SIZE of 200000.
Use MAX_INDIV_PROP_TABLE_SIZE of 20000.
Use MAX_STACK_SIZE of 65536.
Use MAX_SYMBOLS of 20000.
Use MAX_EXPRESSION_NODES of 256.
Use MAX_LABELS of 200000.
Use MAX_LOCAL_VARIABLES of 256.
```

If you receive a message from the compiler saying that one of these values has been exceeded, all you need to do is write a line at the top of your source code increasing it. (It goes without saying that you should _never_ edit the Standard Rules themselves.) For instance:

```inform7
Use MAX_STATIC_DATA of 360000.
```

With a large game, I’ve had to increase MAX_DICT_ENTRIES to 5000 to make room for more vocabulary words. (MAX_DICT_ENTRIES doesn’t seem to be in the Standard Rules. I have no idea where its default value is defined.)

Increasing a value is easy to do — but you might be wondering, what’s going on here? According to Inform guru Andrew Plotkin, MAX_STATIC_DATA “is the compiler's workspace for array data. I7 uses this for tables, and for storage space for relations, indexed text, dynamic lists, and other on-the-fly work. The short answer is no, [needing to increase it] shouldn’t alarm you; 360 kilobytes is pocket change for computers these days. On the other hand, a future Glulx interpreter running on a phone or a Web browser might not be so sanguine. If you’re doing something which costs a huge amount of memory (such as a many-to-many relation), and it’s not necessary [to your game], getting rid of it can only help performance.”
