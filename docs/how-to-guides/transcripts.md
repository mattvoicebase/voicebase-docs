# Transcripts

Once processing is complete, transcripts can be retrieved in several formats.

Note: Export a mediaId and your api token prior to running any of the following examples.

```bash
export MEDIA_ID='The media id of a \
    processed media file (`status` = `finished`)'
export TOKEN='Your Api Token'
```


## JSON Transcript

Retrieve a JSON-formatted transcript with metadata using a `GET` against the `transcripts` collection under the `media` item. By convention, the transcript for most common scenarios is called `latest`.

Make a GET on the /media/$MEDIA_ID/transcripts/latest resource.

```sh
  curl https://apis.voicebase.com/v2-beta/media/$MEDIA_ID/transcripts/latest \
    --header "Authorization: Bearer ${TOKEN}" 
```

##### Example Response
In this example, the agent spoke first, and said "Hello" and the caller spoke second and said "Hi".
Speaker identification is enabled by multi-channel audio, where each channel is associated with a specific speaker. For more information on how to use multi-speaker audio, see the [stereo](stereo.md) section.

###### How to read it
* "p" = Position (word # in the transcript)
* "c" = Confidence (A value between 0-1 that relates to the confidence percent ex: 0.88 = 88%.  When the metadata flag is present confidence contains an arbireary value.)
* "s" = Start time (milliseconds)
* "e" = End time (milliseconds)
* "w" = The word itself (When the metadata flag is present "w" refers to the speaker)
* "m" = metadata (In this case when "m": "turn" it is detecting a change in speaker)

```json
{  
   "transcripts":{  
      "latest":{  
         "revision":"1aa96aa6-7400-45c5-b390-3c5ff2476779",
         "words":[  
            {  
               "p":1,
               "c":0.1,
               "s":2200,
               "e":2350,
               "w":"agent: ",
               "m":"turn"
            },
            {  
               "p":2,
               "c":0.537,
               "s":2200,
               "e":2300,
               "w":"Hello"
            },
            {  
               "p":52,
               "c":0.1,
               "s":2400,
               "e":2550,
               "w":"caller: ",
               "m":"turn"
            },
            {  
               "p":53,
               "c":0.975,
               "s":2400,
               "e":2500,
               "w":"Hi"
            }
         ]
      }
   }
}
```

## Plain Text Transcript

To download a transcript as plain text, add an `Accept` HTTP header with the value `text/plain`.

```sh
curl https://apis.voicebase.com/v2-beta/media/$MEDIA_ID/transcripts/latest \
    --header "Authorization: Bearer ${TOKEN}" \
    --header "Accept: text/plain"
```

## SRT transcript

To retrieve a transcripts as plain text, add an `Accept` HTTP header with the value `text/srt`.

```sh
curl https://apis.voicebase.com/v2-beta/media/$MEDIA_ID/transcripts/latest \
    --header "Authorization: Bearer ${TOKEN}" \
    --header "Accept: text/srt"
```

The [closed captioning](closed-captioning.html) section has a detailed discussion of the SRT transcript format.
