---
title: Find restaurants in NYC except Midtown
description: >-
  Exclude a specific area from results. Use `filter.exclude.location.query`
  alongside `filter.location.query` to return results from a city while cutting
  out a neighborhood or district.
hidden: false
recipe:
  color: '#013365'
  icon: 🔍
---
```curl cURL
curl --request GET \
  --url 'https://api.qloo.com/v2/insights/?filter.type=urn:entity:place \
  &filter.location.query=New York City \
  &filter.exclude.location.query=Midtown \
  &signal.interests.entities=[ENTITY_ID] \
  &take=10' \
  --header 'X-Api-Key: <<apiKey>>'
```

```json Response Example
{
  "success": true,
  "results": {
    "entities": [
      {
        "name": "Roberta's",
        "entity_id": "...",
        "type": "urn:entity",
        "subtype": "urn:entity:place",
        "query": {
          "affinity": 0.95
        }
      }
    ]
  }
}
```

# Pass a location and an exclusion

<!-- curl@3-4 -->



# Add signal to personalize within the area

<!-- curl@5 -->



# Handle the response

<!-- curl@ -->

Results fall within the location boundary and outside the excluded area. Each result includes an affinity score if a signal entity was provided.