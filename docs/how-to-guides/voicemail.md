
# Visual Voicemail


VoiceBase is able to return automatic transcripts for voicemail recordings which can then be delivered via email or SMS.

Below is an optimized configuration for fast and accurate voicemail transcription. This includes features that benefit shorter forms of audio, however they are all optional.

* **Disable [Phrase Groups and Topic Extraction](keywordsandtopics.md):** Disabling sematic processing improves turnaround time and is generally not needed for short files.
* **Enable [Number Formatting](numberformatting.md):** This will format numbers as digits instead of words and adds US phone number formatting which will enable click-to-call for users.
* **Use [Callbacks](callbacks.md):** By using callbacks, our servers will send the data as soon as processing is finished. You won't have to wait until the next polling interval.


## Example Configuration for Voicemail
```json
{  
   "configuration":{  
      "keywords":{  
         "semantic":false
      },
      "topics":{  
         "semantic":false
      },
      "transcripts":{  
         "formatNumbers":[  
            "digits",
            "dashed"
         ]
      },
      "publish":{  
         "callbacks":[  
            {  
               "url":"https://example.com/",
               "method":"POST",
               "include":[  
                  "transcripts"
               ]
            }
         ]
      }
   }
}
```

Now your customers can quickly scan and read through the important parts of their voicemail messages without having to listen to every single recording in their inbox!
Here's a quick [how-to video](https://youtu.be/K9NeLdOAdY4) using Twilio recording. 