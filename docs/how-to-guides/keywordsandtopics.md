# Keywords and Topics


VoiceBase can discover the keywords, key phrases, and topics in your recording using a processing known as semantic indexing ("semantic keywords and topics"). You also have the option of defining groups of keywords or key phrases, which are flagged when they are spotted in the recording.

Export `TOKEN` prior to running any of the following examples.

```bash
export TOKEN='Your Api Token'
```

## Semantic Keywords and Topics

Semantic keywords and topics are discovered automatically (for languages where the feature is supported) and returned with the analytics. For example, the `media.keywords.latest.words` section may contain an entry like the following:

```json
{
  "name": "subscription",
  "t": {
    "caller": [
      "34.48",
      "57.34"
    ],
    "agent": [
      "40.01"
    ]
  },
  "relevance": "0.17"
}
```

In this example, the keyword "subscription" was spoken by the caller around 34 and 57 seconds into the recording, and by the agent around 40 seconds into the recording.

## Managing Keyword Groups

Voicebase allows you to specify pre-defined groups of keywords (or key phrases), which can be used to flag recordings of interest using keyword spotting.

To define new keyword group, or update an existing keyword group, simply PUT the group under /definitions/keywords/groups. The body of the PUT request is a JSON object (`Content-Type: application/json`) that contains two keys:

 - `name` : the name of the keyword group
 - `keywords` : an array of the included keywords

For example, to create group 'data' that includes the keywords data science, big data, and data mining, make the following PUT request using curl, or an equivalent request using a tool of your choice:

```bash
curl https://apis.voicebase.com/v2-beta/definitions/keywords/groups/data \
  --request PUT \
  --header "Content-Type: application/json" \  
  --data '{ "name" : "data", "keywords" : [ "data science", "big data", "data mining" ] }' \
  --header "Authorization: Bearer ${TOKEN}"
```
## Displaying Keyword Groups

To display keyword groups that you have created make the following GET request using curl, or an equivalent request using a tool of your choice:

```bash
curl https://apis.voicebase.com/v2-beta/definitions/keywords/groups/data \
  --request GET \
  --header "Authorization: Bearer ${TOKEN}"
```

The response will look like the following:

```json
{
	"name": "data",
	"revision": "24f20f87-e05d-437a-8436-38e16280d464",
	"keywords": [ "data science", "big data", "data mining" ]
}
```

Revision is the uniqueID that VoiceBase uses applies to each keyword group that can be used to monitor the group.

## Enabling Keyword Spotting

To upload media with keyword spotting enabled, include a JSON configuration attachment with your media POST. The configuration attachment should contain the key:

 - `configuration` : root object for configuration data
    - `keywords` : object for keyword-specific configuration
        - `groups` : array of keyword-spotting groups

For example:

```json
{
  "configuration": {
    "keywords": {
      "groups": [ "data" ]
    }  
  }
}
```

## Disabling Semantic Keywords and Topics

Adding keywords and topics to your media post configuration, enables semantic keywords and topic extraction.

The configuration attachment should contain the key:

 - `configuration` : root object for configuration data
    - `keywords` : object for keyword-specific configuration
        - `semantic` : flag to control semantic keywords
    - `topics` : object for topic-specific configuration
        - `semantic` : flag to control semantic topics

For example:

```json
{  
  "configuration": {
    "keywords": {  
      "semantic": false,
    },
    "topics": {
      "semantic": false
    }
  }
}
```

## Examples

### Example: Defining and spotting a keyword group


Define a `keyword group` by making a PUT request to the `/definitions/keywords/groups/data` resource.

```bash

curl https://apis.voicebase.com/v2-beta/definitions/keywords/groups/data \
  --request PUT \
  --header "Content-Type: application/json" \  
  --data '{ "name" : "data", "keywords" : [ "data science", "big data", "data mining" ] }' \
  --header "Authorization: Bearer ${TOKEN}"
```

Upload media from a local file called recording.mp3 and spot keywords using the `data` group, make the following POST request to `/media`

```bash
curl https://apis.voicebase.com/v2-beta/media \
  --header "Authorization: Bearer ${TOKEN}" \
  --form media=@recording.mp3 \
  --form 'configuration={ "configuration": { "keywords": { "groups": [ "data" ] } } }'
```

### Example: Disabling semantic keywords and topics

The following is an example of posting a media document with semantic `keywords` and `topics` extraction disabled.

```bash
curl https://apis.voicebase.com/v2-beta/media \
  --header "Authorization: Bearer $TOKEN" \
  --form media=@recording.mp3 \
  --form 'configuration={"configuration":{
    "keywords":{ "semantic": false },
    "topics":{ "semantic": false }
  }}'
```
