# Number Formatting

VoiceBase can transcribe numbers found in the transcription be displayed in digit form.

To enable number-formatting, include the following snippet in your configuration:

```json
{  
   "configuration":{  
      "transcripts":{  
         "formatNumbers":true
      }
   }
}
```

Number formatting allows options for transcription preference around phone numbers, currency, addresses, and more. The current version transcribes number words to symbols and US phone number formatting.

For example, with a default configuration, a transcript might read:

>Agent: The total of your bill comes to one hundred thirty eight dollars and sixty five cents

When number formatting is enabled it will read:

>Agent: The total of your bill comes to $138.65

Additionally, VoiceBase can detect phone numbers and format them into a US phone number format within the transcript.

Without number formatting enabled, a plain-text transcript will look like:

>Hi this is Brian from VoiceBase please give me a call back at six five zero two four eight nine six five two thank you.


A plain-text transcript with number formatting enabled:

>Hi this is Brian from VoiceBase please give me a call back at 650-248-9652 thank you.

And an excerpt of the number-formatted JSON response:
For simplicity, start time, end time, & confidence key-values are omitted.
```json
          {
            "p": 12,
            "w": "call"
          },
          {
            "p": 13,
            "w": "back"
          },
          {
            "p": 14,
            "w": "at"
          },
          {
            "p": 15,
            "w": "650-248-9652"
          },
```
As you can see in the JSON response, the phone number will be returned in one word value with the time-stamp beginning at the first digit said and ending at the last digit.
