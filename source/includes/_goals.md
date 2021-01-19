# Goals

## Get Goals

```shell
curl https://<your-company>.workpath.com/api/v1/goals?query=become&start_date=2019-04-01&end_date=2019-06-30
  -H "Authorization: Token <your-api-token>"
```

> The above command returns JSON structured like this:<br>Status: 200 OK<br>Content-Type: application/json

```json
{
  "goals": [
    {
      "confidence_level": 9,
      "description": null,
      "id": 1,
      "kind": "organization",
      "last_status_update_at": "2019-04-26T17:11:16Z",
      "owner": "Bernd Miksch",
      "progress": 0.83,
      "start_date": "2019-04-01",
      "target_date": "2019-06-30",
      "team": null,
      "team_id": null,
      "title": "Become a recognized key player in our industry"
    },
    {
      "confidence_level": 10,
      "description": null,
      "id": 6,
      "kind": "team",
      "last_status_update_at": "2019-04-26T17:11:14Z",
      "owner": "Elena Wischer",
      "progress": 0.19,
      "start_date": "2019-04-01",
      "target_date": "2019-06-30",
      "team": "Marketing",
      "team_id": 4,
      "title": "Become a well-known and admired social media brand"
    }
  ],
  "pagination": {
    "current_page": 1,
    "items_per_page": 25,
    "total_pages": 1,
    "total_items": 2
  }
}
```

This endpoint retrieves all goals filtered by the given parameters.

### HTTP Request

`GET https://<your-company>.workpath.com/api/v1/goals`

### Query Parameters

| Parameter | Type | Need | Description |
|-----------|------|------|-------------|
| `start_date` | string | required when `end_date` given | `start_date` of the date range filter. Format: `YYYY-MM-DD`. When omitted all goals with `target_date` in the future are returned |
| `end_date` | string | required when `start_date` given | `end_date` of the date range filter. Format: `YYYY-MM-DD`. When omitted all goals with `target_date` in the future are returned |
| `team_id` | integer | optional | `id` of a Workpath team. When set only goals owned by that team will be returned |
| `query` | string | optional | `query` to search against goal title, goal description, all key_result titles and all key_result descriptions |
| `page` | integer | optional | number of a specific page. First page will be returned when omitted or out of range |

## Get Goal Details

```shell
curl https://<your-company>.workpath.com/api/v1/goals/1
  -H "Authorization: Token <your-api-token>"
```

> The above command returns JSON structured like this:<br>Status: 200 OK<br>Content-Type: application/json

```json
{
  "confidence_level": 9,
  "description": null,
  "draft": false,
  "goal_children_ids": [2, 3],
  "goal_parents_ids": [],
  "id": 1,
  "initiatives": [
    {
      "description": null,
      "id": 1,
      "last_status_update_at": "2019-06-28T10:39:29Z",
      "owner": "Bernd Miksch",
      "status": "in_progress",
      "title": "Raise brand awareness among target group"
    }
  ],
  "key_results": [
    {
      "confidence_level": 10,
      "currency": null,
      "current_value": 10,
      "description": null,
      "id": 1,
      "last_status_update_at": null,
      "milestones": [],
      "owner": null,
      "owner_team": null,
      "progress": 1,
      "start_value": 7,
      "target_value": 10,
      "title": "Generate 10% of our revenues through recommendations",
      "type": "percental"
    }
  ],
  "kind": "organization",
  "last_status_update_at": "2019-06-27T12:01:54Z",
  "owner": "Bernd Miksch",
  "progress": 0.83,
  "progress_calculation": "key_results",
  "labels": [
    "Strategic Initiative 1"
  ],
  "start_date": "2019-04-01",
  "secret": false,
  "target_date": "2019-06-30",
  "team": null,
  "title": "Become a recognized key player in our industry"
}
```

### HTTP Request

`GET https://<your-company>.workpath.com/api/v1/goals/<goal-id>`

### Query Parameters

| Parameter | Type | Need | Description |
|-----------|------|------|-------------|
| `goal_id` | integer | required in path | `id` of the `goal` to show details for |
