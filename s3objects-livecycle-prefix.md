***S3 Lifecycle prefix for objects***
✅ Core Lifecycle Concepts
Lifecycle rules automate actions like transitioning storage class or expiring objects based on time since creation or versioning status.

Rules apply to objects using a filter, which can include:

Prefix (e.g., logs/)

Tags

Object size filters

Logical AND combinations

📁 Using Prefixes
You can apply lifecycle actions to objects with a shared key prefix:

Example: Archive and Delete by Prefix

📆 Lifecycle Action Types
Transition: Move to cheaper storage (e.g., Glacier, Standard-IA).

Expiration: Permanently delete the object.

AbortIncompleteMultipartUpload: Clean up uploads not completed.

NoncurrentVersionTransition / Expiration: Manage older versions in versioning-enabled buckets.

ExpiredObjectDeleteMarker: Remove unnecessary delete markers.

📌 Advanced Filtering

🧪 Examples of Lifecycle Strategies
Tiering over time: Move from Standard → Standard-IA → Glacier.

Version control: Keep only the last N versions or delete old versions after X days.

Small object transitions: Must explicitly allow transitioning objects <128KB (post-Sept 2024).

Disable rules temporarily with <Status>Disabled</Status>.

⚠️ Important Behaviors
Deletion overrides transition.

Only one filter per rule, but you can combine conditions.

Objects can match multiple rules, so precedence matters.

Versioned buckets need special handling for delete markers.



✅ 1. Transition and Expire Objects by Prefix
Transition objects under logs/ to Glacier after 30 days and delete after 365 days:

```
{
  "Rules": [
    {
      "ID": "LogsToGlacierAndExpire",
      "Filter": {
        "Prefix": "logs/"
      },
      "Status": "Enabled",
      "Transitions": [
        {
          "Days": 30,
          "StorageClass": "GLACIER"
        }
      ],
      "Expiration": {
        "Days": 365
      }
    }
  ]
}
```
✅ 2. Multiple Rules with Different Prefixes
```
{
  "Rules": [
    {
      "ID": "ClassA_Rule",
      "Filter": {
        "Prefix": "classA/"
      },
      "Status": "Enabled",
      "Transitions": [
        {
          "Days": 365,
          "StorageClass": "GLACIER"
        }
      ],
      "Expiration": {
        "Days": 3650
      }
    },
    {
      "ID": "ClassB_Rule",
      "Filter": {
        "Prefix": "classB/"
      },
      "Status": "Enabled",
      "Transitions": [
        {
          "Days": 90,
          "StorageClass": "STANDARD_IA"
        }
      ],
      "Expiration": {
        "Days": 365
      }
    }
  ]
}
```
✅ 3. Lifecycle Rule for Versioning-Enabled Bucket
```
{
  "Rules": [
    {
      "ID": "VersionedRule",
      "Filter": {
        "Prefix": ""
      },
      "Status": "Enabled",
      "Transitions": [
        {
          "Days": 90,
          "StorageClass": "STANDARD_IA"
        }
      ],
      "NoncurrentVersionTransitions": [
        {
          "NoncurrentDays": 30,
          "StorageClass": "GLACIER"
        }
      ],
      "NoncurrentVersionExpiration": {
        "NoncurrentDays": 365,
        "NewerNoncurrentVersions": 5
      }
    }
  ]
}
```
✅ 4. Remove Expired Delete Markers (Versioned Bucket)
```
{
  "Rules": [
    {
      "ID": "RemoveExpiredMarkers",
      "Filter": {
        "Prefix": "logs/"
      },
      "Status": "Enabled",
      "Expiration": {
        "ExpiredObjectDeleteMarker": true
      }
    }
  ]
} ```
✅ 5. Abort Incomplete Multipart Uploads
```
{
  "Rules": [
    {
      "ID": "AbortMultipartUploads",
      "Filter": {
        "Prefix": "temp/"
      },
      "Status": "Enabled",
      "AbortIncompleteMultipartUpload": {
        "DaysAfterInitiation": 7
      }
    }
  ]
}
```
