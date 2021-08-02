## Large Text Blocks {#large-text-blocks}

Inform has an upper limit of about 3,000 characters on how much text can be included between quotation marks as a single chunk. You might run into this limit, for instance, while writing a long intro to your story (which many players frown on) or while writing an explanation for new players of how to play IF (a courteous and useful thing to do).

The way to work around this limit is to create an object and give it several properties that are all blocks of text. Here’s the intro of my game “A Flustered Duck” — not the intro itself, but the structure I created to print it out:

```inform7
When play begins: say "[intro-1 of the text-holder][intro-2 of the text-holder][intro-3 of the text-holder]".

The text-holder is a thing. The text-holder has some text called intro-1\. The text-holder has some text called intro-2\. The text-holder has some text called intro-3.

intro-1 of the text-holder is "'Elliott! Elliott! Where are you, boy?' Granny Grabby's screeching voice rouses you from your pleasant, drowsy contemplation of a moth that has blundered into the barn and is flitting aimlessly about, trying to find its way back outdoors. [...and so on...]”
```
