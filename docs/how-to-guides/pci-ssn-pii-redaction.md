# PCI, SSN, PII Redaction


VoiceBase allows you to redact sensitive data (after [detecting it](pci-ssn-pii-detection.html)) from your recordings, transcripts, and analytics.


### Transcript redaction

To redact sensitive information from a media file, upload it to Voicebase, with a redact section in the detector configuration. In this example, any words in the detected region will be replaced with `[redacted]`.

```json
{ 
  "detections": [
    {
      "model": "PCI",
      "redact": {
        "transcripts": "[redacted]"
      }
    }
  ]
}
```

### Analytics redaction

Sensitive data is automatically redacted from analytics (such as keywords and topics) when transcript redaction is enabled. No additional configuration is needed. 

### Audio redaction

To redact sensitive regions from your recording, upload it to VoiceBase, and add an `audio` section to the detector's redaction configuration. In this example, sensitive audio regions will be replaced with a 270 Hz tone of moderate volume.


```json
{ 
  "detections": [
    {
      "model": "PCI",
      "redact": {
        "transcripts": "[redacted]",
        "audio": {
          "tone": 270,
          "gain": 0.5
        }
      }
    }
  ]
}
```

To download the redacted audio, make a GET request to media/{mediaId}/streams. The response will be of the form:

```json
{
  "streams": {
    "original": "https://link.to.redacted.media"
  }
}

```

An expiring link to download the audio file with redacted will appear in place of *https://link.to.redacted.media*.

### Examples

#### Transcript Redaction Request

```bash
curl https://apis.voicebase.com/v2-beta/media \
  --form media=@recording.mp3 \
  --form configuration='{
    "configuration": {
      "detections": [
        {
          "model": "PCI",
          "redact": {
            "transcripts": "[redacted]"
          }
        },
        {
          "model": "SSN",
          "redact": {
            "transcripts": "[redacted]"
          }
        }
      ]
    }
  }' \
  --header "Authorization: Bearer ${TOKEN}" 
```

#### Audio Redaction Request

```bash
curl https://apis.voicebase.com/v2-beta/media \
  --form media=@recording.mp3 \
  --form configuration='{
    "configuration": {
      "detections": [
        {
          "model": "PCI",
          "redact": {
            "transcripts": "[redacted]",
            "audio": {
              "tone": 270,
              "gain": 0.5
            }
          }
        },
        {
          "model": "SSN",
          "redact": {
            "transcripts": "[redacted]",
            "audio": {
              "tone": 270,
              "gain": 0.5
            }
          }
        }
      ]
    }
  }' \
  --header "Authorization: Bearer ${TOKEN}"
```

#### Redacted Audio Request

```bash
curl https://apis.voicebase.com/v2-beta/media/${MEDIA_ID}/streams \
  --header "Authorization: Bearer ${TOKEN}"
```

