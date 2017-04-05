
# Custom Vocabulary

Voicebase has a unique feature that can increase the possibility of terms or phrases being transcribed by the VoiceBase speech engine resulting in better accuracy.

The feature is used to preferentially transcribe:

* Jargon
* Proper Nouns (Names, Companies, etc.)
* Acronyms
* Non-dictionary words
* Hyphenated words 
* Multi-word phrases

For example, company names, last name or alternative spellings may not be present in the standard dictionary. Those can be added and given preferential treatment to be transcribed. Words that already exist in the dictionary can be added to custom vocabulary to give them preferential treatment to be transcribed.

Upon a standard configuration, a submitted audio file may return a transcript such as:

“Hi this is Brian from voice space.”

However using Custom Vocabulary, we can specify that we would want the company name “VoiceBase” to be recognized.  We can do so using the ad-hoc method of Custom Vocabulary below:

```json
{ "configuration": 
	{ 
		"executor": "v2", 
		"transcripts": 
			{
				"vocabularies": [ { "terms" : [ "VoiceBase" ] } ] 
			} 
	}
}
```

When processed with the Custom Vocabulary configuration, the returned transcript would read

“Hi, this is Brian from VoiceBase.”

## Limitations: 

Currently, Custom Vocabulary has a limit of 1000 terms per file processed. Greater than 1000 terms runs the risk of noticeable degradation in turnaround time and accuracy.

Note: The greater the amount of custom vocabulary terms the greater the chance the overall accuracy may go down, even while the custom vocabulary accuracy goes up. 

## Upload Scenarios:

There are two ways to upload custom vocabulary terms to VoiceBase:

### Ad-hoc Scenario 

If you have a voice file to transcribe and want to add ad hoc custom terms specifically for that file, upload the file with the following configuration:
```json
      {
         "configuration": {
              "executor": "v2",
              "transcripts": {
                 "vocabularies": [
                     {
                        "terms" : [
                           "Bob Okunski", 
                           "Chuck Boynton",
                           "Tom Werner"
                        ]
                     }
                 ]
             }
          }
      } 
```

### Pre-Defined List:

You can add a re-usable custom vocabulary list to your VoiceBase account with a PUT request to /definitions/transcripts/vocabularies/($VOCABLISTNAME) with Content-Type application/JSON and the following body:

```json
 {
           "vocabulary" : {
               "name": "earningsCalls",
               "terms": [
                     "AFFO",
                     "APAC",
                     "CapEx"
               ]
           }
       }
```

From this example, the Custom Vocabulary list is named “earningsCalls”, and can be now be used in configurations attached with all media uploads.  To attach a pre-defined custom vocabulary list to media files, use the configuration below:   (Note* this can also be combined with adhoc terms)

```json
{  
   "configuration":{  
      "transcripts":{  
         "engine":"premium",
         "vocabularies":[  
            {  
               "name":"earningsCalls"
            }
         ]
      }
   }
}
```

## Example cURL Request:

```bash
curl https://apis.voicebase.com/v2-beta/definitions/transcripts/vocabularies/companies \
  --request PUT \
  --header "Content-Type: application/json" \
  --header "Authorization: Bearer ${TOKEN}" \
  --data '{  
   "vocabulary":{  
        "name": "earningsCalls",
		"terms": [
                     "AFFO",
                     "APAC",
                     "CapEx"
                 ]
   }
}'
```

Example successful response on PUT request:

```json
{
  "_links": {
    "self": {
      "href": "/v2-beta/definitions/transcripts/vocabularies/earningsCalls"
    }
  },
  "name": "companies",
  "revision": "4c15602e-3966-4b05-81f0-0d4f18436dee",
  "terms": [
    "AFFO",
    "APAC",
    "CapEx"
  ]
}
```



 



