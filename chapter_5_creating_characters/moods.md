## Moods {#moods}

Real people can get into a variety of moods — friendly, bored, hostile, romantic, frightened, twitchy, and so on. The extension Mood Variations by Emily Short provides an easy way to switch characters from one mood to another in the course of conversation. It’s meant to be used with a conversation package such as Eric Eve’s Conversation Framework, but you don’t need to actually use the features in Conversation Framework or Conversation Responses if you don’t want to; you just need to include one of them so that Mood Variations can make use of a variable called the current interlocutor. Mood Variations is set up to make it easy to switch a character’s mood in the course of conversation, using the syntax “[set hostile]” within a quote. This will always set the mood of the person the player is currently talking to. To change a character’s mood outside of quotes, you need to write something like, “now the current mood of Bob is hostile”.

Here’s a short game, which makes not a bit of sense, but may give you a quick idea of what’s possible if you include Mood Variations. The “asked-or-told about” syntax is defined in Conversation Responses. Notice that the first thing we do is define a list of moods. This will include all of the moods that _any_ character can get into in the game. We don’t create a separate list of moods for each character.

```ìnform7
Include Conversation Responses by Eric Eve.
Include Mood Variations by Emily Short.

The moods are friendly, neutral, bored, hostile, and frightened. The current mood of a person is usually neutral.

The Test Lab is a room. "Many devious tests are conducted here."

The player carries an apple and a pear.

Susan is a woman in the Lab. Dave is a man in the Lab.

Response of Susan when asked-or-told about the pear:
        if the current mood of Susan is neutral:
                say "[set friendly]'That's quite a pear, there,' Susan replies.";
                now the current mood of Dave is hostile;
        otherwise if the current mood of Susan is friendly:
                say "[set hostile]'I love that you keep asking me that,' she says.";
        otherwise if the current mood of Susan is hostile:
                say "'Do shut up,' Susan snaps."

Response of Dave when asked-or-told about the apple:
        if the current mood of Dave is neutral:
                say "[set bored]'I saw one once, in Eden,' Dave replies.";
        otherwise if the current mood of Dave is bored:
                say "[set hostile]Dave yawns ostentatiously.";
        otherwise if the current mood of Dave is hostile:
                say "'Are you trying to pick a fight?' Dave asks.";
        otherwise:
                say "'Apples, apples....'"
