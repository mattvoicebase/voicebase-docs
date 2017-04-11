
# Custom Vocabulary

##### Summary
VoiceBase allows you to customize the speech engine to correctly recognize words and phrases that you would not find in a standard dictionary. Using this, you can have the flexibility of a highly tuned, and even more accurate speech engine for specific verticals and vernacular.

##### Use Case
The Custom Vocabulary feature is most useful for:
* Jargon
* Proper Nouns (names, products, companies, street and city names, etc.)
* Acronyms
* Non-dictionary words
* Hyphenated words
* Multi-word phrases

Let's consider a simple message:

>Hi this is Bryon from VoiceBase.

Let's look at how to use Custom Vocabulary to help ensure that Bryon (an uncommon spelling) and VoiceBase are correctly recognized. The name Bryon can be input from a CRM system, along with

Using the ad-hoc method of Custom Vocabulary we can add these terms as part of the request configuration file:

```json
{ "configuration":
	{
		"executor": "v2",
		"transcripts":
			{
				"vocabularies": [ { "terms" : [ "Bryon" , "VoiceBase" ] } ]
			}
	}
}
```

When processed with the Custom Vocabulary configuration, the returned transcript would read

“Hi, this is Bryon from VoiceBase.”



There are two ways to upload custom vocabulary terms to VoiceBase:

### Ad-Hoc Scenario

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

### Pre-Defined List

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

From this example, the Custom Vocabulary list is named “earningsCalls”, and can be now be used in configurations attached with all media uploads.  To attach a pre-defined custom vocabulary list to media files, use the configuration below:   (**Note** this can also be combined with adhoc terms)

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

## Limitations

* Currently, Custom Vocabulary has a limit of 1000 terms per file processed. Greater than 1000 terms runs the risk of noticeable degradation in turnaround time and accuracy.

**Note:** Since Bryon is a non-standard way of the common name Brian, we would not want to include this term for every call, but VoiceBase allows you to create vocabularies specific for each file. In this way, you can submit names of people, streets, cities, products, and industry or company specific terms from a CRM system or other data source which are useful in this call, but will not affect others.


## Example cURL Request

```bash
curl https://apis.voicebase.com/v2-beta/definitions/transcripts/vocabularies/earningsCalls \
  --request PUT \
  --header "Content-Type: application/json" \
  --header "Authorization: Bearer ${TOKEN}" \
  --data '{  
    "vocabulary": {  
      "name": "earningsCalls",
		  "terms": [
        "AFFO",
        "APAC",
        "CapEx"
      ]
    }
  }'
```

## Example successful response to PUT request

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
