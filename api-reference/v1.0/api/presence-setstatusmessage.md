---
title: "presence: setStatusMessage"
description: "Set a presence status message for a user."
author: "afedorov"
ms.localizationpriority: medium
doc_type: apiPageType
ms.prod: "cloud-communications"
---

# presence: setStatusMessage

Namespace: microsoft.graph

Set a presence status message for a user. An optional expiration date and time can be supplied.

## Permissions
The following permission is required to call the API. To learn more, including how to choose permissions, see [Permissions](/graph/permissions-reference).

| Permission type                        | Permissions (from least to most privileged) |
| :------------------------------------- | :------------------------------------------ |
| Delegated (work or school account)     | Presence.ReadWrite                          |
| Delegated (personal Microsoft account) | Not supported.                              |
| Application                            | Presence.ReadWrite.All                              |

## HTTP Request
<!-- { "blockType": "ignored" } -->
```http
POST /users/{userId}/presence/setStatusMessage
```

## Request headers
| Name          | Description                 |
| :------------ | :-------------------------- |
| Authorization | Bearer {token}. Required.   |
| Content-Type  | application/json. Required. |

## Request body

In the request body, provide a JSON object with the following parameters.

| Parameter       | Type            |  Description                                 |
| --------------- | --------------- |------------------------------------------- |
| `statusMessage` | [microsoft.graph.presenceStatusMessage](../resources/presencestatusmessage.md) | Contains the presence status message of the user. |

## Response
If successful, this method returns a `200 OK` response code.

## Examples

### Example 1: Set status message with expiry date

The following request sets the presence status message as "Hey I'm currently in a meeting." for user `fa8bf3dc-eca7-46b7-bad1-db199b62afc3`, with the expiration on `2022-10-18 at 17:05:33.2079781 Pacific Standard Time`.

#### Request


<!-- {
  "blockType": "request",
  "name": "setstatusmessage"
}-->

```msgraph-interactive
POST https://graph.microsoft.com/v1.0/users/fa8bf3dc-eca7-46b7-bad1-db199b62afc3/presence/setStatusMessage
Content-Type: application/json

{
  "statusMessage": {
    "message": {
        "content": "Hey I'm currently in a meeting.",
        "contentType": "text"
    },
    "expiryDateTime": {
        "dateTime": "2022-10-18T17:05:33.2079781",
        "timeZone": "Pacific Standard Time"
    }
  }
}
```

---

#### Response

<!-- {
  "blockType": "response",
  "name": "setstatusmessage",
  "truncated": true
} -->
```http
HTTP/1.1 200 OK
```

### Example 2: Set status message of another user

The following request sets the presence status message as "Hey I am available now" for user `fa8bf3dc-eca7-46b7-bad1-db199b62afc3`. In Example 3, presence information for user `fa8bf3dc-eca7-46b7-bad1-db199b62afc3` is obtained on behalf of another user via a [getPresence](presence-get.md) request.

#### Request

<!-- {
  "blockType": "request",
  "name": "setstatusmessage-another-user"
}-->
```msgraph-interactive
POST https://graph.microsoft.com/v1.0/users/fa8bf3dc-eca7-46b7-bad1-db199b62afc3/presence/setStatusMessage
Content-Type: application/json

{
  "statusMessage": {
    "message": {
      "content": "Hey I am available now",
      "contentType": "text"
    }
  }
}
```

---

#### Response

<!-- {
  "blockType": "response",
  "name": "setstatusmessage-another-user",
  "truncated": true
} -->
```http
HTTP/1.1 200 OK
```

### Example 3: Get another user presence
This example follows Example 2. Presence information for user `fa8bf3dc-eca7-46b7-bad1-db199b62afc3` is obtained on behalf of another user via a [getPresence](presence-get.md) request.

#### Request

<!-- {
  "blockType": "request",
  "name": "setstatusmessage-another-user-get-presence"
}-->
```msgraph-interactive
GET https://graph.microsoft.com/v1.0/users/fa8bf3dc-eca7-46b7-bad1-db199b62afc3/presence
```

---

#### Response
Because this request gets the presence status for another user, the `statusMessage.expiryDateTime` and `statusMessage.publishedDateTime` properties are not included in the response body.

<!-- {
  "blockType": "response",
  "name": "setstatusmessage-another-user-get-presence",
  "@odata.type": "microsoft.graph.presence",
  "truncated":"true"
} -->
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "id": "fa8bf3dc-eca7-46b7-bad1-db199b62afc3",
  "availability": "Available",
  "activity": "Available",
  "outOfOfficeSettings": {
    "message": null,
    "isOutOfOffice": false
  },
  "statusMessage": {
    "message": {
      "content": "Hey I am available now",
      "contentType": "text"
    }
  }
}
```
