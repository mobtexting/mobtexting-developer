# Messaging

The SMS API supports the following:

#### Note:

As new DLT restrictions effective from Jan 31, we are suggesting to use the Template API for avoiding delivery issues related to DLT, [Goto Template API](/docs/{version}/send-template-sms)

#### HTTP Methods

`POST` - When you send a POST request with the end user's phone number to the messaging subresource, We sends the SMS message you specify.

`GET` - You can retrieve the results of the message you sent using the GET method. You do this by sending a GET request containing the reference id for the message you sent. We return a response message in the form of a _**JSON**_ object in the entity body.

### Services

Types of services and their values are listed below:

- T - Transactional Messaging.
- P - Promotional Messaging.
- S - Transcrub Messaging.
- G - Global Messaging

Country code is mandatory to be included in the `to` paramenter for global messaging and optional for indian numbers. If country code not found, default `91` will get appended to mobile number.

Before you start sending transactional SMS through this API, please test whether your content is matching a template which has been pre approved. Otherwise, the SMS will end up being rejected.

## Send SMS

#### API Endpoint

```
{domain}/api/{version}/
```

#### POST

```
{endpoint}sms/send
```

#### MANDATORY PARAMETERS

| Name    | Descriptions                                                                            |
| ------- | --------------------------------------------------------------------------------------- |
| to      | Phone number to send with country prefix. (multiple numbers can be separated by comma.) |
| message | The content of the SMS                                                                  |
| sender  | The registered and approved Sender-id                                                   |
| service | Determines whether the SMS to be sent is Transactional, Promotional or other.           |

#### OPTIONAL PARAMETERS

| Name        | Descriptions                                                                                                                                                            |
| ----------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| entity_id   | Principal Entityid registered in DLT portal (applicable for indian routes only)                                                                                         |
| template_id | TemplateId registered in DLT portal (applicable for indian routes only)                                                                                                 |
| webhook_id  | The `id` of the webhook created in Webhook Section for which the SMS response to be sent after delivery report from operator. [read more](/docs/{version}/sms-push-dlr) |
| time        | Schedule time (in format i.e,yyyy-mm-dd hh:mm:ss) at which the SMS has to be sent.                                                                                      |
| type        | The SMS to be sent is Unicode, Normal or Auto detect. (value "U", "N" or "A")                                                                                           |
| flash       | This parameter can be used to send flash sms via API ( Values 1 or 0.)                                                                                                  |
| custom      | Your own unique_id parameters                                                                                                                                           |

| port | Port number to which SMS has to be delivered |

#### Example Request

```
curl -X POST '{endpoint}sms/send' \
    -H 'Accept: application/json' \
    -H 'Authorization: Bearer 38e896f55670311982434e929559bxxxx' \
    -H 'Content-Type: application/x-www-form-urlencoded' \
    -d 'sender=TXTSMS' \
    -d 'to=917026267xxx' \
    -d 'service=T' \
    -d 'message=Your OTP is 123456'
```

#### Example Response

```json
{
  "status": 200,
  "message": "1 numbers accepted for delivery.",
  "data": [
    {
      "id": "b34e35ad-fe34-4a8b-977c-b21cd76cd7d6:1",
      "mobile": "918921269xxx",
      "status": "AWAITING-DLR",
      "units": 1,
      "length": 7,
      "charges": 1,
      "customid": "",
      "iso_code": null,
      "submitted_at": "2018-07-09 16:27:35"
    }
  ]
}
```
