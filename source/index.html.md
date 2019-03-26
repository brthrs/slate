---
title: Messaging API Reference

language_tabs:
  - shell


---

# Introduction

Welcome to the Scheduled Messaging API. You can use it to retreive your messages, create new ones and update or detele them.

We provided basic examples to test the different Messaging APU endpoint.

This API documentation page must and was generated with [Slate](https://github.com/lord/slate)

# Authentication

> To authorize, use the Authorization with every request:

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: scheduledrules"
```

> Make sure to replace `scheduledrules` with your API key.

To use the Message API you need an API key. You can find your personal API key in the [Scheduled Web app settings page](https://webapp.scheduledapp.com/).

The Message API expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: scheduledrules`

<aside class="notice">
You must replace <code>scheduledrules</code> with your personal API key.
</aside>

# Message

## Get All Messages

```shell
curl "https://webapp.scheduledapp.com/api/messages" \
  -H "Authorization: scheduledrules"
```

> The above command returns JSON structured list like this:

```json
[
  {
    "uid": "dJq2jvUOok2FdDxKAt9",
    "text": "Hello There",
    "recipients": [
      {
        "phone": "+316876543210",
        "lastname": "Appleseed",
        "firstname": "John"
      }
    ],
    "spentCredits": 1,
    "repeatMode": "kSCHRepeatModeNone",
    "scheduledDate": "2019-03-31T10:50:25.227Z",
    "autosend": true,
    "archived": true
  },
  {
    "uid": "ouv0JudLkGm8CmS9iKj",
    "text": "Hello Email",
    "recipients": [
      {
        "email": "test@test.com",
        "lastname": "Appleseed",
        "firstname": "John"
      }
    ],
    "spentCredits": 1,
    "repeatMode": "kSCHRepeatModeNone",
    "scheduledDate": "2019-03-11T10:50:25.227Z",
    "autosendemail": true
  },
]
```

This endpoint retrieves all your messages.

### HTTP Request

`GET https://webapp.scheduledapp.com/api/messages


## Get a Specific Message

```shell
curl "https://webapp.scheduledapp.com/api/messages/dJq2jvUOok2FdDxKAt9" \
  -H "Authorization: scheduledrules"
```

> The above command returns JSON structured like this:

```json
{
    "uid": "dJq2jvUOok2FdDxKAt9",
    "text": "Hello There",
    "recipients": [
      {
        "phone": "+316876543210",
        "lastname": "Appleseed",
        "firstname": "John"
      }
    ],
    "spentCredits": 1,
    "repeatMode": "kSCHRepeatModeNone",
    "scheduledDate": "2019-03-31T10:50:25.227Z",
    "autosend": true,
    "archived": true
  }
```

This endpoint retrieves a specific message.

### HTTP Request

`GET https://webapp.scheduledapp.com/api/messages/<UID>`

### URL Parameters

Parameter | Description
--------- | -----------
UID       | The UID of the message to receive


## Create a new Message

```shell
curl "https://webapp.scheduledapp.com/api/messages" \
  -X POST \
  -H "Authorization: scheduledrules" \
  -H 'Content-Type: application/json; charset=utf-8' \
  -d $'{
  "recipients": [
    {
      "firstname": "Jonh",
      "lastname": "Appleseed",
      "phone": "+316876543210"
    }
  ],
  "text": "Hello There",
  "sentDate": "2019-12-30T10:50:25.227Z"
}'
```

> The above command returns JSON structured of the message:

```json
{
  "uid": "ouv0Ju8dLkGm8CmS9iK",
  "text": "Hello There",
  "recipients": [
    {
      "lastname": "Jonh",
      "firstname": "Appleseed",
      "phone": "+316876543210"
    }
  ],
  "spentCredits": 1,
  "repeatMode": "kSCHRepeatModeNone",
  "scheduledDate": "2019-12-30T10:50:25.227Z",
  "autosend": true
}
```

This endpoint creates a new message.

### HTTP Request

`POST https://webapp.scheduledapp.com/api/messages`

### JSON payload key values

| Parameter            | Type   | Required | Description                                                                                                                                                                            |
|----------------------|--------|----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| text                 | String |     *    | The test message you want to send                                                                                                                                                      |
| subject              | String |          | Only used when schedule a email message                                                                                                                                                |
| scheduledDate        | Date   |     *    | Date and time when to send the message                                                                                                                                                 |
| recipients           | Array  |     *    | Array with recipients                                                                                                                                                                  |
| recipients.firstname | String |          | First name of the recipient                                                                                                                                                            |
| recipients.lastname  | String |          | Last name of the recipient                                                                                                                                                             |
| recipients.phone     | String |     *    | Phone number of recipient (required when scheduling sms)                                                                                                                               |
| recipients.email     | String |     *    | Email address of recipient (required when scheduling email)                                                                                                                            |
| repeatMode           | String |          | One of the following: kSCHRepeatModeNone, kSCHRepeatModeDaily, kSCHRepeatModeWeekly,  kSCHRepeatModeMonthly, kSCHRepeatModeYearly, kSCHRepeatModeWeekdays, kSCHRepeatModeEveryTwoWeeks |
| repeatEndDate        | Date   |          | Date and time when the repeat modus must stop                                                                                                                                          |
| autosend             | Bool   |          | Set to true if you want to schedule a sms message                                                                                                                                      |
| autosendemail        | Bool   |          | Set to true if you want to schedule a email message                                                                                                                                    |

## Update a Specific Message

```shell
curl "https://webapp.scheduledapp.com/api/messages/ouv0Ju8dLkGm8CmS9iK" \
  -X PUT \
  -H "Authorization: scheduledrules" \
  -H 'Content-Type: application/json; charset=utf-8' \
  -d $'{
  "recipients": [
    {
      "firstname": "Jonh",
      "lastname": "Appleseed",
      "phone": "+316876543210"
    }
  ],
  "text": "Hello There",
  "sentDate": "2019-12-31T10:50:25.227Z"
}'
```

> The above command returns JSON structured like this:

```json
{
  "uid": "ouv0Ju8dLkGm8CmS9iK",
  "text": "Hello There",
  "recipients": [
    {
      "lastname": "Jonh",
      "firstname": "Appleseed",
      "phone": "+316876543210"
    }
  ],
  "spentCredits": 1,
  "repeatMode": "kSCHRepeatModeNone",
  "scheduledDate": "2019-12-31T10:50:25.227Z",
  "autosend": true
}
```

This endpoint retrieves a specific message.

### HTTP Request

`PUT https://webapp.scheduledapp.com/api/messages/<UID>`

### URL Parameters

Parameter | Description
--------- | -----------
UID | The UID of the message to receive

### JSON payload key values

| Parameter            | Type   | Required | Description                                                                                                                                                                            |
|----------------------|--------|----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| text                 | String |     *    | The test message you want to send                                                                                                                                                      |
| subject              | String |          | Only used when schedule a email message                                                                                                                                                |
| scheduledDate        | Date   |     *    | Date and time when to send the message                                                                                                                                                 |
| recipients           | Array  |     *    | Array with recipients                                                                                                                                                                  |
| recipients.firstname | String |          | First name of the recipient                                                                                                                                                            |
| recipients.lastname  | String |          | Last name of the recipient                                                                                                                                                             |
| recipients.phone     | String |     *    | Phone number of recipient (required when scheduling sms)                                                                                                                               |
| recipients.email     | String |     *    | Email address of recipient (required when scheduling email)                                                                                                                            |
| repeatMode           | String |          | One of the following: kSCHRepeatModeNone, kSCHRepeatModeDaily, kSCHRepeatModeWeekly,  kSCHRepeatModeMonthly, kSCHRepeatModeYearly, kSCHRepeatModeWeekdays, kSCHRepeatModeEveryTwoWeeks |
| repeatEndDate        | Date   |          | Date and time when the repeat modus must stop                                                                                                                                          |
| autosend             | Bool   |          | Set to true if you want to schedule a sms message                                                                                                                                      |
| autosendemail        | Bool   |          | Set to true if you want to schedule a email message                                                                                                                                    |


## Delete a Specific Message

```shell
curl "https://webapp.scheduledapp.com/api/messages/ouv0Ju8dLkGm8CmS9iK" \
  -X DELETE \
  -H "Authorization: scheduledrules" \
```

> The above command returns JSON structured like this:

```json
{
  "id": "ouv0Ju8dLkGm8CmS9iK",
  "deleted" : true
}
```

This endpoint deletes a specific message.

### HTTP Request

`DELETE https://webapp.scheduledapp.com/api/messages/<UID>`

### URL Parameters

Parameter | Description
--------- | -----------
UID | The UID of the message to receive
