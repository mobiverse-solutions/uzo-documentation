---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: home
---

#### USSD Flow 
To initiate a USSD session, the user dials a USSD code from their mobile handset. The Telco USSD Gateway receives the request and routes it to Uzo. Uzo then sends the request to the client's application URL using HTTP POST method with json data. The client's application URL is the endpoint that handles the USSD logic and responds to the user's input.

![ussd-message-flow](/assets/images/ussd-flow.png){:class="img-responsive"}




#### The Uzo POST request body

```json
{
    "ussdString" : "*1234#", 
    "msisdn" : "+233111111111",
    "ussdServiceOp" : "1", 
    "sessionId" : "12341235123",
    "network" : "06"
}
```

**msisdn:** The phone number of the requester

**ussdString:** The input provided by the requester. For initiating requests this will always be the
USSD query string eg.*1234#

**sessionID:** Session ID for the USSD transaction

**ussdServiceOp:** This determines the kind of request. The following are the values and their meanings:

| Value             | Description          |
|-------------------|----------------------|
| `1`               | initiating request   |
| `18`              | continuing request   |
| `29 or greater`   | terminating request  |



**network:** This value identifies the network provider from which the request is coming. The value
is the MNC of the network provider. Follow this link [https://mcc-mnc-list.com/list](https://mcc-mnc-list.com/list){:target="_blank"}{:rel="noopener noreferrer"} to see a list of networks and corresponding
MNCs


#### The Client App response body

```json
{
    "message" : "Welcome\n1 Say hello\n2 Exit", 
    "ussdServiceOp" : 1
}
```

**message:** Message to be sent back to user's phone screen. This is your app menu, etc.

**ussdServiceOp:** This defines the type of response. The valid values and their meanings are below: 

| Value             | Description          |
|-------------------|----------------------|
| `2`               | continuing response  |
| `17`              | final response       |


