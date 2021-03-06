
# **OpenDirect (OOH) Webhook Standardization**

**Version history**

| **Version** | **Date** | **Changes** | **Author**|
| --- | --- | --- | --- |
| v1.0 | Nov 12th, 2020 | First version describing how a webhook set-up should be standardized in an implementation of the OpenDirect (OOH) standard. All changes and versioning of this document will now be handled in Github |Tim Harvey|


## Table of Contents

[Introduction & Context](#introduction--context) 

[Key Contributers](#key-contributers) 

[cOOHding.Club Members](#coohdingclub-members) 

[Process Summary](#process-summary) 

[Webhooks](#webhooks) 

[Anatomy of a webhook message](#anatomy-of-a-webhook-message) ([Headers](#headers), [Encoding](#encoding), [Events & Payloads](#events--payloads), [Example Message](#example-message), [Body](#body) )

[Sending Webhook Messages](#sending-webhook-messages) ([Retry Mechanism](#retry-mechanism))

[Receiving messages](#receiving-messages) ([Returning the correct response code](#_x4ikkfd533rl))

[Securing Webhooks](#securing-webhooks) ([HMAC](#hmac),
[Canonicalized Headers](#canonicalized-headers),
[Registering The Shared Key](#registering-the-shared-key),
[Reccomendations](#recommendations),
[IP-Whitelisting](#ip-whitelisting))

## Introduction & Context

[The OOH OpenDirect standard](https://github.com/Outsmart-OOH/ooh_open_direct) suggests webhook feedback for several operations. This document describes how to set these up and how they should behave, thus standardizing implementation of webhooks in an implementation of [the OOH OpenDirect standard](https://github.com/Outsmart-OOH/ooh_open_direct).

This document is limited to anything that relates to platform & technology independent mechanisms, purely to facilitate easy, reliable, efficient and secure communication between two Open Direct v1.5.1 systems.

## Key Contributers
* Sebastiaan Schinkel, Signkick
* Alex Radu, Posterscope

## cOOhding.Club Members
* Anant East, Talon
* Denis Garcia, Global
* Rob Brayshaw, Global
* Matt Allard, Global
* Ioana Dima, VIOOH
* Jack Paget, VIOOH
* Joao Baptista, Clearchannel 
* Karen Fornos Klein, Clearchannel 
* Miles Talmey, Clearchannel
* Luka Djukic, Ocean Outdoor
* Prasaant Patel, Kinetic
* Rebecca Lee, JCDecaux
* Steve Pavett, Posterscope
* Daniel Conway, Posterscope

## Process Summary

The diagram below shows a summary flow of the webhook functional process in the form of a `GET /stats` request (Campaign Order Line upsite and performance report request)

![Process Summary](pictures/Diagram1.png)


## Webhooks

For asynchronous processing within the OpenDirect standard, webhooks offer a way to receive instant notifications on updates for any of these operations. Within the current OpenDirect (OOH) 1.5.1 standard, this is mostly needed for order line status changes and change requests, usually awaiting manual intervention.

Polling could be used as an alternative for the webhooks. The current OpenDirect (OOH) 1.5.1 v1.1 standard already facilitates this.

The image below is taken from OpenDirect (OOH) 1.5.1 v1.1, and shows which state transitions require a webhook callback.

![Use of Webhooks in OpenDirect(OOH)](pictures/Diagram2.png)


## Anatomy of a webhook message

### Encoding
Default encoding should be Unicode (UTF-8).

### Headers

The `application/json` content type should be used for all messages.

The following headers are used to send meta-information about what kind of event is sent, if it the message is retried, and security information:

| **Header name** | **Description** |
| --- | --- |
| `Authorization` | HMAC-SHA512 signature of the message for sender authenticity verification |
| `X-OohWebhook-Event` | Name of the event, e.g. &#39;OrderLineStateChange&#39;. For now, this seems to also be the only event that needs to be supported. |
| `X-OohWebhook-MessageId` | A UUID for the event instance. Should be kept the same across redeliveries of the same event instance, see &#39;delivery id&#39; below. For each new webhook call that is not a retry, a new message-id should be generated. |
| `X-OohWebhook-DeliveryId` | A UUID for a single call to a webhook. This is useful to identify redeliveries of the same event instance (so having the same event-id), if supported &amp; enabled at the caller for the callee. |

### Events & Payloads

Events & payloads can be found throughout the OOH OpenDirect standard. The payload of webhook messages should be the same as their corresponding GET endpoints. All webhook supported messages need a corresponding GET endpoint to alsofacilitate long-polling and/or a manual refresh of information.


### Example message

_Headers_
```json
"Authorization": "NjRiN2JlMzIzZTNmM2ZmZTRkZDMxNmMzMmYyNTI5MTAwNzkyZmFjMmNhODJmMGYyZjYxN2JmMTA5NzVjMmQwMzA1YzhhODI4MjYzNWU4OTA5YWNhMjMzYjg3YTNkYWE5ZTdiYzE5MTBiYTBjODRhYTE1YWFmM2EzODViNDFmZjQ"
"X-OohWebhook-Event": "OrderLine.ReservationConfirmed"
"X-OohWebhook-EventId": "5778e93f-2905-4b61-bba1-443ac6410b3c"
"X-OohWebhook-DeliveryId": "10c18c70-a76a-4254-a7b6-d9ec86a5ffd5"
```
### Body

```json
{
    "$schema": "https://raw.githubusercontent.com/Outsmart-OOH/ooh_open_direct/master/schema/v1/uris/lines/lines_response.json",
    
    "BookingStatus": "Reserved",
    "StateChangeReason": "",
    "Comment": "Free form comment",
    "Cost": 8000,
    "EndDate": "2014-12-10T18:00:00.000Z",
    "Id": "345233",
    "Name": "My Line 1",
    "OrderId": "1235872",
    "ProductId": "456366",
    "OOHProviderData":  { "PoNumber": "88873" } ,
    "StartDate": "2014-12-05T06:00:00.000Z",
    "Targeting": [
        {
            "Name": "Inventory",
            "Type": "Frames",
            "DataSource": "Space",
            "Target": "frame_id",
            "TargetValues": [
                "1234931339",
                "1235190735",
                "1234931338",
                "1235191547"
                ]
        },
        {
            "Name": "Delivery",
            "Type": "Frames",
            "DataSource": "Time",
            "Target": "Days",
            "TargetValues": [ "5", "6" ]
        },
        {
            "Name": "Delivery",
            "Type": "Frames",
            "DataSource": "ShareOfDisplay",
            "Target": "ShareOfTime",
            "TargetValues": ["20"]

        },
        {
            "Name": "Delivery",
            "Type": "Frames",
            "DataSource": "ShareOfDisplay",
            "Target": "Spot",
            "TargetValues": ["5"]

        }

    ]
}
```

## Sending webhook messages

For a system offering a OpenDirect OOH API, the starting point is that for any message supporting webhook feedback, a URI is sent in the request body using the field &quot;webhook&quot;. When an event is triggered in the OpenDirect system supporting webhook feedback, it should send a message using the HTTP POST method to the webhook URI that was sent with the original request.

For each unique event, a unique message identifier should be generated to populate the `X-OohWebhook-MessageId` header, and the message needs to be signed as described in the &quot;Securing webhooks&quot; section.

The payload can be exactly the same as the payload that would normally send back in a direct response.

### Retry mechanism

In case of an error response or time-out, the caller should try to deliver the request multiple times. An error is assumed when the HTTP-response status code from the endpoint is not within the 2xx range, or when a time-out occurs. It's recommended to default to 3 retries/redeliveries, with an incremental time delay between them, e.g. 5 seconds, 30 seconds and 120 seconds. For each retry/redelivery a unique delivery UUID should be sent in the X-OohWebhook-DeliveryId HTTP header, to be able to distinguish between different delivery attempts.

## Receiving messages

To receive a message as an OpenDirect client, the OpenDirect client needs to communicate a webhook URI to the OpenDirect server. A field for this called &quot;webhook&quot; is present on any request that facilitates this.

If a webhook URI is communicated, a message will be sent to that URI when an underlying resource has been updated. When the OpenDirect client receives a message, the first thing that needs to happen is to check the message authenticity by checking if the message was signed correctly, as outlined in [Securing webhooks](#securing-webhooks).

The next step should be to verify if the message hasn&#39;t already been processed. `The X-OohWebhook-MessageId` and `X-OohWebhook-DeliveryId` fields can be used to determine this. Both fields should probably be logged for each incoming request to be able to easily debug webhook message processing. Unique webhook events will have a unique message id, and should only be processed once. The delivery id can be used to discern different delivery attempts of the same message.

If the message is signed properly, and hasn&#39;t already been processed, the next step will be to actually process the message. To know what to do with the webhook request, the `X-OohWebhook-Event` HTTP header can be inspected, to determine the type of the event. Based on this, the message can be processed according to the documentation that is set-up for each resource type in the OpenDirect OOH standard.

### Returning the correct response code

For the retry mechanism to properly function, a HTTP response code in the 200 range should be returned when the message is properly received. In most cases, it&#39;s probably best to return a 200 response code if the message is processed synchronously, and a 202 response code if the message is handled asynchronously, e.g. added to a queue to be processed later.

## Securing webhooks

Next to using HTTPS to encrypt the communication, additional security measures can be taken to properly secure the webhook calls.

### HMAC

HMAC is a way to verify if the message is coming from a trusted sender, and that its contents haven&#39;t been changed since it was sent. In order to be able to verify the sender of the incoming calls, a SecretKey in the form of a UUID must be shared between both the client and server systems. The SecretKey could either be provided by the organisation offering the API, or configured in a UI of the OD151 system by the client system organization.

Based on the request body (payload) and the shared SecretKey, an HMAC (hash-based message authentication code) signature should be generated by the calling system and provided in the &quot;Authorization&quot; HTTP header, using the SHA512 hash function.

The receiving system can validate the authenticity of the incoming message by using the SecretKey, the webhook headers and the body of the received message to generate a new HMAC, and compare it with the one provided from the calling system in order to ensure that it comes from a trusted sender.

_The algorithm_

The following algorithm should be used for computing the authorization signature:

```js
sha512(
    secret-key,
    message-body + "\n" +
    canonicalized-ooh-webhook-headers
)
```

Where:

- `secret-key` represents the secret key agreed upon by the buyer &amp; seller
- `message-body` represents the request message payload
- `canonicalized-ooh-webhook-headers` represents the canonicalized headers
- `sha512` represents the hashing function-based message authentication code using the SHA512 cryptographic hashing algorithm and the secret key

### Canonicalized Headers

The webhook headers should be canonicalized, so that both buyer &amp; seller include in the same way when hashing the message. The headers should be canonicalized by:

- Lower-casing the header names,
- Sorting the headers ascending by name ascending,
- Removing any newlines (`\n`) in the header value,
- Separating each header headers by newlines (`\n`),
- Not adding any outer quotes in both keys and values.

_Example:_

Given the message headers:

```json
"X-OohWebhook-DeliveryId": "10c18c70-a76a-4254-a7b6-d9ec86a5ffd5"
"X-OohWebhook-Event":      "OrderLine.ReservationConfirmed"
"X-OohWebhook-EventId":    "5778e93f-2905-4b61-bba1-443ac6410b3c"
```

And message body:

```json
{
    "myExampleKeyInJsonBody": "myExampleValueInJsonBody"
}
```

And secret key:

    a135cee0-b260-4d38-93cf-540ed564a527

The hash should be computed as follows:

```js
sha512(
    "a135cee0-b260-4d38-93cf-540ed564a527",
    "{\"myExampleKeyInJsonBody\": \"myExampleValueInJsonBody\"}\nx-oohwebhook-deliveryid:10c18c70-a76a-4254-a7b6-d9ec86a5ffd5\nx-oohwebhook-event:OrderLine.ReservationConfirmed\nx-oohwebhook-eventid:5778e93f-2905-4b61-bba1-443ac6410b3c"
)
```

### Registering the Shared Key

To be able to sign and verify messages using HMAC, a shared key is needed. This key has to be generated once, and should be refreshed at least every couple of months or so. The shared key needed for HMAC signing, can be generated by either the buyer or the seller. They could be exchanged in an automated way by e.g. an API, but any secure way of exchanging the key will do.

![Registering the Shared Key](pictures/Diagram3.png)

### Recommendations

The shared cryptographic secret key should be different for each buyer.

### IP-whitelisting

Additionally, IP-whitelisting could be set-up to secure the webhook endpoints. Since this can be circumvented using IP-spoofing, it&#39;s recommended that it is used in combination with content signing using HMAC.
