# Anki card generation by using AI

The prompt in `./generateVocabularyPrompt.txt` will generate a CSV ready to be imported to a Anki deck.
A sample of the Anki deck is attached (`./ankiDeck.apkg`)

The recordings for the cards are generated using Azure Speech Service by utilizing the HyperTTS addon.

## Settings for English vocabulary (Hyper-TTS)

Regex for correct pauses between sentences necessary.

| Type  | Pattern | Replacement                     |
| ----- | ------- | ------------------------------- |
| Regex | `"\."`  | `"<break strength="medium" />"` |

## Settings for Japanese vocabulary (Hyper-TTS)

- The first regex will insert a pause between two sentences
- The second regex will help Azure Speed Service to choose the correct reading of Kanji<br>
  It will replace the kanji with the reading which must be defined in square brackets after the kanji.<br>
  e.g.<br>
  レストランは空[す]いています。<br>
  レストランは`<sub alias="す">空</sub>`いています。<br>

| Type  | Pattern                 | Replacement                     |
| ----- | ----------------------- | ------------------------------- |
| Regex | `"。"`                  | `"<break strength="medium" />"` |
| Regex | `"([^ [\]]+)\[(.*?)\]"` | `"<sub alias="\2">\1</sub>"`    |

Source: https://www.vocab.ai/tutorials/hypertts-tips-for-japanese