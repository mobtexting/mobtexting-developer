# SMS Api Using File

The SMS API supports the following:

#### HTTP Methods

`POST` - When you send a POST request with file containing mobile numbers of customers, We send SMS message you specify to all the numbers exist in file.

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
{endpoint}sms/bulk
```

You can send sms using `POST` method only as uploading file will supporting in
`POST`.

#### MANDATORY PARAMETERS

| Name    | Descriptions                                                                                                |
| ------- | ----------------------------------------------------------------------------------------------------------- |
| message | The content of the SMS                                                                                      |
| sender  | The registered and approved Sender-id                                                                       |
| service | Determines whether the SMS to be sent is Transactional, Promotional or other.                               |
| file    | Request body form-data you need to select file parameter and need to upload file containing mobile numbers. |

#### OPTIONAL PARAMETERS

| Name        | Descriptions                                                                                                                                                           |
| ----------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| webhook_id  | The `id` of the webhook created in Webhook Section for which the SMS response to be sent after delivery report from operator. read more](/docs/{version}/sms-push-dlr) |
| time        | Schedule time (in format i.e,yyyy-mm-dd hh:mm:ss) at which the SMS has to be sent.                                                                                     |
| type        | The SMS to be sent is Unicode, Normal or Auto detect. (value "U", "N" or "A")                                                                                          |
| flash       | This parameter can be used to send flash sms via API ( Values 1 or 0.)                                                                                                 |
| custom      | Any customised parameters can be passed using this parameter                                                                                                           |
| port        | Port number to which SMS has to be sent                                                                                                                                |
| column      | Mobile number column name same as in customize sms                                                                                                                     |
| entity_id   | Principal Entityid registered in DLT portal                                                                                                                            |
| template_id | TemplateId registered in DLT portal                                                                                                                                    |

#### Example Request

```
curl -X POST \
  '{endpoint}sms/bulk' \
    -H 'Accept: application/json' \
    -H 'Authorization: Bearer 38e896f55670311982434e929559bxxxx' \
    -H 'content-type: multipart/form-data; boundary=----WebKitFormBoundary7MA4YWxkTrZu0gW' \
    -d 'sender=TXTSMS' \
    -d 'to=917026267xxx' \
    -d 'service=T' \
    -d 'message=Your OTP is 123456'
    -F file=@filename.txt
```

#### Example Response

```json
{
  "status": 200,
  "message": "XXX numbers accepted for delivery.",
  "data": []
}
```
