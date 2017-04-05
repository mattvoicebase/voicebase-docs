# Number Formatting

Voicebase has the ability to have numbers found in the transcription be displayed in digit form.

To enable number-formatting, include the following snippet in your configuration:

```json
{"configuration":{"transcripts":{"formatNumbers":true}}}
```

Number formatting allows options for transcription preference around phone numbers, currency, addresses, and more. The current version transcribes number words to symbols and US phone number formatting.

For example, with a standard configuration with number formatting by default turned off.  A transcript might read:

>Agent: The total of your bill comes to one hundred thirty eight dollars and sixty five cents

When number formatting is enabled it will read:

>Agent: The total of your bill comes to $138.65

Additionally, Voicebase can detect phone numbers and format them into a US phone number format within the transcript.

With number formatting not enabled a plain-text response will look like:

>Hi this is Brian from VoiceBase please give me a call back at six five zero two four eight nine six five two thank you. Goodbye.

And an excerpt of the JSON transcript response would look like:
```json
{
            "p": 12,
            "s": 4060,
            "c": 0.917,
            "e": 4320,
            "w": "call"
          },
          {
            "p": 13,
            "s": 4320,
            "c": 0.728,
            "e": 4669,
            "w": "back"
          },
          {
            "p": 14,
            "s": 4700,
            "c": 0.658,
            "e": 4980,
            "w": "at"
          },
          {
            "p": 15,
            "s": 5010,
            "c": 0.938,
            "e": 5469,
            "w": "six"
          },
          {
            "p": 16,
            "s": 5470,
            "c": 0.891,
            "e": 5860,
            "w": "five"
          },
          {
            "p": 17,
            "s": 5860,
            "c": 0.943,
            "e": 6370,
            "w": "zero"
          },
          {
            "p": 18,
            "s": 6740,
            "c": 0.071,
            "e": 7130,
            "w": "to"
          },
          {
            "p": 19,
            "s": 7160,
            "c": 0.962,
            "e": 7500,
            "w": "four"
          },
          {
            "p": 20,
            "s": 7530,
            "c": 0.893,
            "e": 7930,
            "w": "eight"
          },
          {
            "p": 21,
            "s": 8260,
            "c": 0.984,
            "e": 8640,
            "w": "nine"
          },
          {
            "p": 22,
            "s": 8640,
            "c": 0.929,
            "e": 9210,
            "w": "six"
          },
          {
            "p": 23,
            "s": 9250,
            "c": 0.894,
            "e": 9590,
            "w": "five"
          },
          {
            "p": 24,
            "s": 9590,
            "c": 0.255,
            "e": 9970,
            "w": "to"
          }
```

Here is the plain-text response with number formatting turned on:

>Hi this is Brian from VoiceBase please give me a call back at 650-248-9652 thank you. Goodbye.

And an excerpt of the number-formatted JSON response:
```json
          {
            "p": 12,
            "s": 4060,
            "c": 0.917,
            "e": 4320,
            "w": "call"
          },
          {
            "p": 13,
            "s": 4320,
            "c": 0.728,
            "e": 4669,
            "w": "back"
          },
          {
            "p": 14,
            "s": 4700,
            "c": 0.658,
            "e": 4980,
            "w": "at"
          },
          {
            "p": 15,
            "s": 5010,
            "c": 0.95,
            "e": 9970,
            "w": "650-248-9652"
          },
```
As you can see in the JSON response, the phone number will be returned in one “word” value with the time-stamp beginning at the first digit said and ending at the last digit.
