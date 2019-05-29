
# Introduction

Welcome to the Workpath API documentation. This API can be used to build custom clients that integrate with the Workpath platform.

# Current Version

The current API version is `v1`. It is available at `https://<your-company>.workpath.com/api/v1`.

If you don't know `<your-company>` subdomain, you can <a href="https://www.workpath.com/en/retrieve-account" target="_blank">retrieve it with your Workpath user email address</a>.

# Authentication

> Authentication example:

```shell
curl https://<your-company>.workpath.com/api/v1/<endpoint>
  -H "Authorization: Token <your-api-token>"
```

> Make sure to replace `<your-api-token>` with your API token.

The Workpath API uses tokens to grant access. A guide how to create an API Client and API Token can be found in the <a href="https://workpath.zendesk.com/hc/en-us/articles/360023684614-Public-API" target="_blank">Workpath Help Center</a>.

When creating an API Client you have to specify a Workpath user whos access rights will be used when requesting the API. Attributes that are not accessible for this user will be returned as `null`.

Once you have obtained the API Token, include it in the Authorization header.

| Header | Value |
|--------|-------|
| Authorization | `Token <your-api-token>` |

# Schema

The API enforces `JSON` format.
Make sure to set the following headers with every request:

| Header | Value | Comment |
|--------|-------|---------|
| Accept | `application/json` ||
| Content-Type | `application/json` | for `POST` or `PATCH` requests |

If not specified the API will respond `406 Not Acceptable`.

Blank fields are included as `null` instead of being omitted.

All dates and timestamps are returned in ISO 8601 format: `YYYY-MM-DDTHH:MM:SSZ`

# Pagination

```json
{
  "goals": [...],
  "pagination": {
    "current_page": 2,
    "items_per_page": 25,
    "total_pages": 6,
    "total_items": 139
  }
}
```

All endpoints returning multiple items include a pagination object. Add the parameter `?page=2` to your request to access a specific page.

# Errors

> Error messages are returned like this:<br>Status: 422 Unprocessable Entity<br>Content-Type: application/json

```json
{
  "errors": [
    {
      "attribute": "end_date",
      "code": "blank",
      "message": "End date can't be blank"
    }
  ]
}
```

The Workpath API uses the following error codes:

Code | Meaning
---- | -------
400 | Bad Request -- Your request is invalid.
401 | Unauthorized -- Your API token is wrong.
403 | Forbidden -- You don't have access to this resource.
404 | Not Found -- The specified resource could not be found.
406 | Not Acceptable -- You requested a format that isn't JSON.
422 | Unprocessable Entity -- See the JSON error response body for details.
500 | Internal Server Error -- You found an edge case and we will fix it as soon as possible. Please try again later.
503 | Service Unavailable -- We are temporarily offline for maintenance. Please try again later.
