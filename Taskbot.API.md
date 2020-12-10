  | Change Version | API Version | Change nots | Change Date | Author |
  | - | - | - | - | - |
  | 1.0 | v1 | Taskbot API V1 | 2020-12-10 | Light |


# Summary
  - Taskbot
    - [session](#session)  


# Session
  - `POST /api/v1/bot/taskbot/{taskbotId}/createSession` - [Create session](#create-session)
  - `POST /api/v3/bot/taskbot/{sessionId}:triggerSession` - [Trigger Session](#trigger-session)
  - `POST /api/v3/bot/taskbot/{sessionId}:submitInformation` - [Submit Information](#submit-information)
  - `POST /api/v3/bot/taskbot/{sessionId}:submitAuthentication` -  [Submit Authentication](#submit-authentication)
  - `POST /api/v3/bot/taskbot/{sessionId}:submitLocation` - [Submit Location](#submit-location)
  - `POST /api/v3/bot/taskbot/{sessionId}:endSession` - [End Session](#end-session)

## Related Object Json Format

### TaskbotSession Object
  TaskbotSession Object is represented as simple flat JSON objects with the following keys:  

  |Name| Type | Default | Description     | 
  | - | - | :-: | - | 
  | `sessionId` | Guid  | | sessionId |
  | `message` |  [TaskbotMessage](#TaskbotMessage-Object) Object |  | message |
  | `context` | [TaskbotContext](#TaskbotContext-Object) Object  |   | context |

### TaskbotContext Object
  TaskbotContext Object is represented as simple flat JSON objects with the following keys:  

  |Name| Type | Default | Description     | 
  | - | - | :-: | - |   
  | `taskbotId` | Guid  | | taskbotId |
  | `taskbotVersionId` | Guid  | | current session versionId of taskbot  |
  | `authentication` | string  | | authentication data |
  | `location` | string  | | the longitude and latitude of the location, e.g. "-39.900000,116.300000" |
  | `variableValues` | [NameValueCollection](#NameValue-object)[] |  | an array of [NameValue](#NameValue-object) objects |
  | `latestMessage` | [TaskbotMessage](#TaskbotMessage-Object)   | | record path and save collected info  |

### NameValueCollection Object
FieldValue is represented as simple flat json objects with the following keys:

|Name| Type|  Default |  Description     |
| - | - | :-: |  - | 
|`name` | string |  | the name of variable. |
|`value` | string |  | the value of variable. |


### TaskbotMessage Object
  TaskbotMessage Object is represented as simple flat JSON objects with the following keys:  

  |Name| Type| Default | Description     | 
  | - | - | :-: | - | 
  | `id` | Guid  |  | the unique id of the response |
  | `type` | string  |  | type of the response,including `sendMessage`,`quickReply`、 `sendImage`、`sendVideo`、`ssoLoginButton`,`collectLocation`, `collectInfo`,`collectVariableData`,`bookMeeting`,`transferChat` |
  | `content` | object |  | response's content. when type is `sendMessage`, it represents [SendMessage](#SendMessage-object); when type is `quickReply`,it represents [QuickReply](#QuickReply-object);when type is `sendImage`,it represents [SendImage](#SendImage-object);when type is `sendVideo`,it represents [SendVideo](#SendVideo-Object); when type is `ssoLoginButton`, it represents [SSOLoginButton](#SSOLoginButton-Object);when type is `collectLocation`, it represents [CollectLocation](#CollectLocation-Object);when type is `collectInfo`, it represents [CollectInfo](#CollectInfo-Object);when type is `collectVariableData`, it represents [CollectVariableData](#CollectVariableData-Object);when type is `bookMeeting`, it represents [BookMeeting](#BookMeeting-Object);when type is `transferChat`, it represents [TransferChat](#TransferChat-Object);|


###  SendMessage Object
  Smart Trigger Action is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Default | Description |
  | - | - | :-: | - |
  | `typingDelay` | decimal |  |  float (0.0-10.0). Default: 1.0. The typing delay in seconds before this message is shown in chat window. Visitor can see bot is typing in chat window |  
  | `message` | string | | HTML Text.  |
  | `buttons` | [MessageButton](#MessageButton-Object)[] |  | message buttons |
  | `nextActionId` | guid | | next Taskbot Ation Id |


### MessageButton Object
  MessageButton is represented as simple flat json objects with the following keys:

  |Name| Type | Default | Description     | 
  | - | - | :-: | - | 
  | `buttonText` | string  | |  String (256).  |
  | `type` | string  |  | enums:`link`, `webview`|
  | `url` | string  |  | String (2048).   |
  | `openIn` | string  |  | enums:`currentWindow`, `newWindow`, `sideWindow`|
  | `openStyle` | string  |  | enums:`compact`, `tall`|
  | `order` | int  |  | order  |

###  QuickReply Object

   QuickReply is represented as simple flat JSON objects with the following keys:

  | Name | Type | Default | Description |
  | - | - | - | - |
  | `typingDelay` | decimal |  |  float (0.0-10.0). Default: 1.0. The typing delay in seconds before this message is shown in chat window. Visitor can see bot is typing in chat window |  
  | `message` | string | | HTML Text.  |
  | `options` | [QuickReplyOption](#QuickReplyOption-Object)[] |  | options |
  | `OtherResponseToActionId` | guid | | Task Bot Action. The action to go to when visitor replies with any other message |
  

### QuickReplyOption Object

  QuickReplyOption is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Default | Description |    
  | - | - | - | - | 
  | `Text` | strubg |  |   String (256). |  
  | `NextActionId` | guid | |  |
  | `Order` | int | | Order Number|
  


### SendImage Object

  SendImage is represented as simple flat JSON objects with the following keys:  

  | Name | Type |  Default | Description |    
  | - | - | - | - | 
  | `typingDelay` | decimal |  |  float (0.0-10.0). Default: 1.0. The typing delay in seconds before this message is shown in chat window. Visitor can see bot is typing in chat window |  
  | `message` | string | | HTML Text.  |
  | `imageUrl` | string | | url  |
  | `NextActionId` | guid | | NextActionId |

###  SendVideo Object

  SendVideo is represented as simple flat JSON objects with the following keys:  

  | Name | Type |  Default | Description |    
  | - | - | - | - | 
  | `typingDelay` | decimal |  |  float (0.0-10.0). Default: 1.0. The typing delay in seconds before this message is shown in chat window. Visitor can see bot is typing in chat window |  
  | `message` | string | | HTML Text.  |
  | `videoUrl` | string | | url  |
  | `NextActionId` | guid | | NextActionId |

###  SSOLoginButton Object

   SSOLoginButton is represented as simple flat JSON objects with the following keys:  

  | Name | Type |  Default | Description |    
  | - | - | - | - | 
  | `typingDelay` | decimal |  |  float (0.0-10.0). Default: 1.0. The typing delay in seconds before this message is shown in chat window. Visitor can see bot is typing in chat window |  
  | `message` | string | | HTML Text.  |
  | `loginButtonText` | string | |   loginButtonText|
  | `loginInActionId` | guid | |  loginInActionId |
  | `failedActionId` | guid | |  failedActionId |


###  CollectLocation Object

   CollectLocation is represented as simple flat JSON objects with the following keys:  

  | Name | Type  | Default | Description |    
  | - | - | :-: | - | 
  | `typingDelay` | decimal |  |  float (0.0-10.0). Default: 1.0. The typing delay in seconds before this message is shown in chat window. Visitor can see bot is typing in chat window |  
  | `message` | string | | HTML Text.  |
  | `buttonText` | string  |  | text of the location button |
  | `successActionId` | guid | |  successActionId |
  | `failedActionId` | guid | |  failedActionId |


###  CollectInfo Object

   CollectInfo is represented as simple flat JSON objects with the following keys:  

  | Name | Type  | Default | Description |    
  | - | - | :-: | - | 
  | `typingDelay` | decimal |  |  float (0.0-10.0). Default: 1.0. The typing delay in seconds before this message is shown in chat window. Visitor can see bot is typing in chat window |  
  | `message` | string  |  | message of the sign in |
  | `type` | string  |  | enums:`name`, `email`, `phoneNumber`, `companyName`, `comment`|
  | `nextActionId` | guid | | NextActionId |


###  CollectVariableData Object

   CollectVariableData is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Default | Description |    
  | - | - | :-: | - | 
  | `typingDelay` | decimal |  |  float (0.0-10.0). Default: 1.0. The typing delay in seconds before this message is shown in chat window. Visitor can see bot is typing in chat window |  
  | `message` | string  |  | message of the sign in |
  | `variableName` | string  |  | variableName |
  | `type` | string  |  | enums:`text`, `textArea`, `radioBox`, `switch`, `dropDownList`, `checkBoxList`, `email`, `password`, `integer`, `decimal`, `date`, `time`|
  | `options` | string  |  | variableName |
  | `nextActionId` | guid | | nextActionId |


###  BookMeeting Object
 BookMeeting is represented as simple flat json objects with the following keys:

|Name| Type| Default | Description     | 
| - | - | :-: | - | 
| `calendlyAccountId` | guid  |  | Calendly Account. |
| `calendlyEventUrl` | string  |  | calendlyEventUrl |
| `successActionId` | guid  |  | Taskbot Action Id |
| `failedActionId` | guid  |  | Taskbot Action Id |
| `nextActionId` | guid | | NextActionId |


###  TransferChat Object
 TransferChat is represented as simple flat json objects with the following keys:

|Name| Type| Default | Description     | 
| - | - | :-: | - | 
| `calendlyAccountId` | guid  |  | Calendly Account. |
| `calendlyEventUrl` | string  |  | calendlyEventUrl |
| `successActionId` | guid  |  | Taskbot Action Id |
| `failedActionId` | guid  |  | Taskbot Action Id |
| `nextActionId` | guid | | NextActionId |


## Endpoints

### Create session
`POST /api/v3/bot/chatbots/{chatbotId}/sessions`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `chatbotId` | Guid | yes  |  the unique id of the bot |  

Request body

The request body contains data with the follow structure:

  | Name | Type | Required | Default | Description |    
  | - | - | :-: | :-: | - | 
  | `channel` | string  | yes | | eg: `Live Chat`, `Facebook Messenger`, `Twitter Direct Message`, `WeChat`, `WhatsApp`, `SMS`, `IVR` |
  | `id` | Guid | yes | |  id of the session, you must generate the unique sessionId  |
  | `context` | [ChatbotSessionContext](#ChatbotSessionContext-Object) Object  | no  |  |

example:
```Json 
  {
    "channel":"IVR",
    "id": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
    "context": {   
      "customData": {
        "name":"Kart",
        "email":"kart@yahoo.com",
        "phone":"123-4355-212",
      }
    }
  }
```

#### Response
the response is: [ChatbotSession](#ChatbotSession-Object) Object


#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "channel":"IVR",
    "id": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
    "context": {   
      "customData": {
        "name":"Kart",
        "email":"kart@yahoo.com",
        "phone":"123-4355-212",
      }
    }
  }' -X POST https://domain.comm100.com/api/v3/bot/chatbots/a9928d68-92e6-4487-a2e8-8234fc9d1f48/sessions
```
Response
```Json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {    
    "channel":"IVR",
    "id": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
    "context": {
      "chatbotId": "a9928d68-92e6-4487-a2e8-8234fc9d1f48",
      "customData": {
        "name":"Kart",
        "email":"kart@yahoo.com",
        "phone":"123-4355-212",
      }
    },
    "message":{
      "id":"d3f5b968-ad51-42af-b759-64c0afc40b84",
      "visitorQuestion":"",
      "type":"greetingMessage",
      "content":{
        "responses":[
          {
            "type":"text",
            "content": {
              "text":"Hi, I'm Peely, I'm glad to help you.",
              "audio":"UklGRrj2AQBXQVZFZm10IBAAAAABAAEAwF0AAIC7AAACABAAZGF0YZT2AQA..."
            }
          },
          {
            "type":"text",
            "content": {
              "text":"You can ask any questions. If you want to know what I can help with, you can say Menu or Options",
              "audio":"UklGRrj2AQBXQVZFZm10IBAAAAABAAEAwF0AAIC7AAACABAAZGF0YZT2AQA..."
            }
          }
        ]
      }
    }    
  }
```

### Detect intent
`POST /api/v3/bot/sessions/{sessionId}:detectIntent`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `sessionId` | Guid | yes  |  id of the chat or conversation |

Request body

The request body contains data with the follow structure:

  | Name | Type | Required | Default | Description |    
  | - | - | :-: | :-: | - | 
  | `channel` | string  | yes | | eg: `Live Chat`, `Facebook Messenger`, `Twitter Direct Message`, `WeChat`, `WhatsApp`, `SMS`, `Voice` |
  | `textInput` | string  | no | | text |
  | `audioInput` | string  | no | | audio, when textInput have value then this is invalid. |
  | `context` | [ChatbotSessionContext](#ChatbotSessionContext-Object) Object  | yes  |  |

example:
```Json 
  {
    "channel":"Facebook Messenger",
    "textInput":"i want to buy NBN",
    "context": {
      "chatbotId": "a9928d68-92e6-4487-a2e8-8234fc9d1f48",
      "customData": {
        "name":"Kart",
        "email":"kart@yahoo.com",
        "phone":"123-4355-212",
      }
    },
  }
```
#### Response
the response is: [ChatbotSession](#ChatbotSession-Object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "channel":"Facebook Messenger",
    "textInput":"i want to buy NBN",
    "context": {
      "chatbotId": "a9928d68-92e6-4487-a2e8-8234fc9d1f48",
      "customData": {
        "name":"Kart",
        "email":"kart@yahoo.com",
        "phone":"123-4355-212",
      }
    },
  }' -X POST https://domain.comm100.com/api/v3/bot/sessions/f9928d68-92e6-4487-a2e8-8234fc9d1f48:detectIntent
```
Response
```Json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {    
    "channel":"Facebook Messenger",
    "id": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
    "context": {
      "chatbotId": "a9928d68-92e6-4487-a2e8-8234fc9d1f48",
      "currentIntentId": "8d6892e6-92e6-4487-a2e8-92e68d6892e6",
      "customData": {
        "name":"Kart",
        "email":"kart@yahoo.com",
        "phone":"123-4355-212",
      }
    },
    "message":{
      "id":"d3f5b968-ad51-42af-b759-64c0afc40b84",
      "visitorQuestion":"i want to buy NBN",
      "type":"highConfidenceAnswer",
      "content":{
        "intentId": "7534fdsca-92e6-4487-a2e8-92e68d6892e6",
        "intentName": "buy nbn",
        "score": 89.25,
        "responses":[
          {
            "type":"htmlText",
            "content": {
              "text":"<div>Hi, what can i do for you?</div>",
            }
          },
          {
            "type":"image",
            "content": {
              "name":"greeting.png",
              "url": "https://bot.comm100.com/botapi/images/greeting.png"
            }
          }
        ]
      }
    }    
  }
```

### Trigger an intent
`POST /api/v3/bot/sessions/{sessionId}:triggerAnIntent`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `sessionId` | Guid | yes  |  id of the chat or conversation |

Request body

The request body contains data with the follow structure:

  | Name | Type | Required | Default | Description |    
  | - | - | :-: | :-: | - | 
  | `channel` | string  | yes | | eg: `Live Chat`, `Facebook Messenger`, `Twitter Direct Message`, `WeChat`, `WhatsApp`, `SMS` |
  | `intentId` | Guid  | yes | | id of the intent triggered |
  | `context` | [ChatbotSessionContext](#ChatbotSessionContext-Object) Object  | yes  |  |

example:
```Json 
  {
    "channel":"Live Chat",
    "intentId":"8d6892e6-92e6-4487-a2e8-92e68d6892e6",
    "context": {
      "chatbotId": "a9928d68-92e6-4487-a2e8-8234fc9d1f48",
      "customData": {
        "name":"Kart",
        "email":"kart@yahoo.com",
        "phone":"123-4355-212",
      }
    }
  }
```

#### Response
the response is: [ChatbotSession](#ChatbotSession-Object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "channel":"Live Chat",
    "intentId":"8d6892e6-92e6-4487-a2e8-92e68d6892e6",
    "context": {
      "chatbotId": "a9928d68-92e6-4487-a2e8-8234fc9d1f48",
      "customData": {
        "name":"Kart",
        "email":"kart@yahoo.com",
        "phone":"123-4355-212",
      }
    }
  }' -X POST https://domain.comm100.com/api/v3/bot/sessions/f9928d68-92e6-4487-a2e8-8234fc9d1f48:triggerAnIntent
```
Response
```Json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {    
    "channel":"Live Chat",
    "id": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
    "context": {
      "chatbotId": "a9928d68-92e6-4487-a2e8-8234fc9d1f48",
      "currentIntentId": "8d6892e6-92e6-4487-a2e8-92e68d6892e6",
      "customData": {
        "name":"Kart",
        "email":"kart@yahoo.com",
        "phone":"123-4355-212",
      }
    },
    "message":{
      "id":"d3f5b968-ad51-42af-b759-64c0afc40b84",
      "visitorQuestion":"Lost Card",
      "type":"authenticationRequest",
      "content":{
        "signInMessage": "Please Login",
        "signInButtonText": "Login",
        "signInURL": "https://domain.comm100.com/ssoidp/ssoLogin.aspx"  
      }
    }    
  }
```

### Submit Authentication
`POST /api/v3/bot/sessions/{sessionId}:submitAuthentication`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `sessionId` | Guid | yes  |  id of the chat or conversation |

Request body

The request body contains data with the follow structure:

  | Name | Type | Required | Default | Description |    
  | - | - | :-: | :-: | - | 
  | `channel` | string  | yes | | eg: `Live Chat`, `Facebook Messenger`, `Twitter Direct Message`, `WeChat`, `WhatsApp`, `SMS`, `Voice` |
  | `authentication` | string  | yes | | authentication data |
  | `context` | [ChatbotSessionContext](#ChatbotSessionContext-Object) Object  | yes  |  |

example:
```Json 
  {
    "channel":"Live Chat",
    "authentication": "vcw1fc9d92e64487a2e892e68d68dsww",
    "context": {
      "chatbotId": "a9928d68-92e6-4487-a2e8-8234fc9d1f48",
      "currentIntentId": "8d6892e6-92e6-4487-a2e8-92e68d6892e6",
      "customData": {
        "name":"Kart",
        "email":"kart@yahoo.com",
        "phone":"123-4355-212",
      }
    }
  }
```

#### Response
the response is: [ChatbotSession](#ChatbotSession-Object) Object


#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "channel":"Live Chat",
    "authentication": "vcw1fc9d92e64487a2e892e68d68dsww",
    "context": {
      "chatbotId": "a9928d68-92e6-4487-a2e8-8234fc9d1f48",
      "currentIntentId": "8d6892e6-92e6-4487-a2e8-92e68d6892e6",
      "customData": {
        "name":"Kart",
        "email":"kart@yahoo.com",
        "phone":"123-4355-212",
      }
    }
  }' -X POST https://domain.comm100.com/api/v3/bot/sessions/f9928d68-92e6-4487-a2e8-8234fc9d1f48:submitAuthentication
```
Response
```Json
  HTTP/1.1 200 OK
  Content-Type:  application/json
{    
    "channel":"Live Chat",
    "id": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
    "context": {
      "chatbotId": "a9928d68-92e6-4487-a2e8-8234fc9d1f48",
      "currentIntentId": "8d6892e6-92e6-4487-a2e8-92e68d6892e6",
      "authentication": "vcw1fc9d92e64487a2e892e68d68dsww",
      "customData": {
        "name":"Kart",
        "email":"kart@yahoo.com",
        "phone":"123-4355-212",
      }
    },
    "message":{
      "id":"d3f5b968-ad51-42af-b759-64c0afc40b84",
      "visitorQuestion":"",
      "type":"locationRequest",
      "content":{
        "message": "Please share your location first.",
        "buttonText": "Share",
      }
    }    
  }
```

### Submit Location
`POST /api/v3/bot/sessions/{sessionId}:submitLocation`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `sessionId` | Guid | yes  |  id of the chat or conversation |

Request body

The request body contains data with the follow structure:

  | Name | Type | Required | Default | Description |    
  | - | - | :-: | :-: | - | 
  | `channel` | string  | yes | | eg: `Live Chat`, `Facebook Messenger`, `Twitter Direct Message`, `WeChat`, `WhatsApp`, `SMS` |
  | `location` | string  | yes | | the longitude and latitude of the location, eg: "39.900000,116.300000" |
  | `context` | [ChatbotSessionContext](#ChatbotSessionContext-Object) Object  | yes  |  |

example:
```Json 
  {
    "channel":"Live Chat",
    "location": "39.900000,116.300000",
    "context": {
      "chatbotId": "a9928d68-92e6-4487-a2e8-8234fc9d1f48",
      "currentIntentId": "8d6892e6-92e6-4487-a2e8-92e68d6892e6",
      "authentication": "vcw1fc9d92e64487a2e892e68d68dsww",
      "customData": {
        "name":"Kart",
        "email":"kart@yahoo.com",
        "phone":"123-4355-212",
      }
    }
  }
```

#### Response
the response is: [ChatbotSession](#ChatbotSession-Object) Object


#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "channel":"Live Chat",
    "location": "39.900000,116.300000",
    "context": {
      "chatbotId": "a9928d68-92e6-4487-a2e8-8234fc9d1f48",
      "currentIntentId": "8d6892e6-92e6-4487-a2e8-92e68d6892e6",
      "authentication": "vcw1fc9d92e64487a2e892e68d68dsww",
      "customData": {
        "name":"Kart",
        "email":"kart@yahoo.com",
        "phone":"123-4355-212",
      }
    }
  }' -X POST https://domain.comm100.com/api/v3/bot/sessions/f9928d68-92e6-4487-a2e8-8234fc9d1f48:submitLocation
```
Response
```Json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {    
    "channel":"Live Chat",
    "id": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
    "context": {
      "chatbotId": "a9928d68-92e6-4487-a2e8-8234fc9d1f48",
      "currentIntentId": "8d6892e6-92e6-4487-a2e8-92e68d6892e6",
      "authentication": "vcw1fc9d92e64487a2e892e68d68dsww",
      "location": "39.900000,116.300000",
      "customData": {
        "name":"Kart",
        "email":"kart@yahoo.com",
        "phone":"123-4355-212",
      }
    },
    "message":{
      "id":"d3f5b968-ad51-42af-b759-64c0afc40b84",
      "visitorQuestion":"",
      "type":"formRequest",
      "content":{
        "message": "Please fill the information first",
        "title": "Fill a Form",
        "isConfirmationRequired": true,
        "fields": [
          {
            "type":"text",
            "name":"email",
            "defaultValue": "kart@yahoo.com",
            "isRequired":true,
            "isMasked":true,
          },
          {
            "type":"dropDownList",
            "name":"city",
            "isRequired":true,
            "isMasked":false,
            "options":["beijing", "hangzhou"],
          }
        ],
      }
    }    
  } 
```

### Submit Form
`POST /api/v3/bot/sessions/{sessionId}:submitForm`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `sessionId` | Guid | yes  |  id of the chat or conversation |

Request body

The request body contains data with the follow structure:

  | Name | Type | Required | Default | Description |    
  | - | - | :-: | :-: | - | 
  | `channel` | string  | yes | | eg: `Live Chat`, `Facebook Messenger`, `Twitter Direct Message`, `WeChat`, `WhatsApp`, `SMS` |
  |`formValues` | [FieldValue](#FieldValue-object)[] | yes | | an array of [FieldValue](#FieldValue-object) objects |
  | `context` | [ChatbotSessionContext](#ChatbotSessionContext-Object) Object  | yes  |  |

example:
```Json 
  {
    "channel":"Live Chat",
    "formValues": [
      {
        "name":"email",
        "value":"kart@yahoo.com",
      },
      {
        "name":"city",
        "value":"beijing",
      },
    ],
    "context": {
      "chatbotId": "a9928d68-92e6-4487-a2e8-8234fc9d1f48",
      "currentIntentId": "8d6892e6-92e6-4487-a2e8-92e68d6892e6",
      "authentication": "vcw1fc9d92e64487a2e892e68d68dsww",
      "location": "39.900000,116.300000",
      "customData": {
        "name":"Kart",
        "email":"kart@yahoo.com",
        "phone":"123-4355-212",
      }
    }
  }  
```

#### Response
the response is: [ChatbotSession](#ChatbotSession-Object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "channel":"Live Chat",
    "formValues": [
      {
        "name":"email",
        "value":"kart@yahoo.com",
      },
      {
        "name":"city",
        "value":"beijing",
      },
    ],
    "context": {
      "chatbotId": "a9928d68-92e6-4487-a2e8-8234fc9d1f48",
      "currentIntentId": "8d6892e6-92e6-4487-a2e8-92e68d6892e6",
      "authentication": "vcw1fc9d92e64487a2e892e68d68dsww",
      "location": "39.900000,116.300000",
      "customData": {
        "name":"Kart",
        "email":"kart@yahoo.com",
        "phone":"123-4355-212",
      }
    }
  }' -X POST https://domain.comm100.com/api/v3/bot/sessions/f9928d68-92e6-4487-a2e8-8234fc9d1f48:submitForm
```
Response
```Json
  HTTP/1.1 200 OK
  Content-Type:  application/json
{    
    "channel":"Live Chat",
    "id": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
    "context": {
      "chatbotId": "a9928d68-92e6-4487-a2e8-8234fc9d1f48",
      "currentIntentId": "8d6892e6-92e6-4487-a2e8-92e68d6892e6",
      "authentication": "vcw1fc9d92e64487a2e892e68d68dsww",
      "location": "39.900000,116.300000",
      "formValues": [
        {
          "name":"email",
          "value":"kart@yahoo.com",
        },
        {
          "name":"city",
          "value":"beijing",
        },
      ],
      "customData": {
        "name":"Kart",
        "email":"kart@yahoo.com",
        "phone":"123-4355-212",
      }
    },
    "message":{
      "id":"d3f5b968-ad51-42af-b759-64c0afc40b84",
      "visitorQuestion":"i want to buy NBN",
      "type":"highConfidenceAnswer",
      "content":{
        "intentId": "7534fdsca-92e6-4487-a2e8-92e68d6892e6",
        "intentName": "buy nbn",
        "score": 89.25,
        "responses":[
          {
            "type":"htmlText",
            "content": "<div>this is your order list</div>"
          },
          {
            "type":"image",
            "content": {
              "name":"greeting.png",
              "url": "https://bot.comm100.com/botapi/images/greeting.png"
            }
          }
        ]
      }
    }    
  }
```

### Submit IVRKey
`POST /api/v3/bot/sessions/{sessionId}:submitIVRKey`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `sessionId` | Guid | yes  |  id of the chat or conversation |

Request body

The request body contains data with the follow structure:

  | Name | Type | Required | Default | Description |    
  | - | - | :-: | :-: | - | 
  | `channel` | string  | yes | | eg:  `IVR` |
  | `key` | string  | yes | | the key of ivr menu |
  | `context` | [ChatbotSessionContext](#ChatbotSessionContext-Object) Object  | yes  |  |

example:
```Json 
  {
    "channel":"IVR",
    "key":"#",
    "context": {
      "chatbotId": "a9928d68-92e6-4487-a2e8-8234fc9d1f48",
      "customData": {
        "name":"Kart",
        "email":"kart@yahoo.com",
        "phone":"123-4355-212",
      }
    }
  }  
```
#### Response
the response is: [ChatbotSession](#ChatbotSession-Object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "channel":"IVR",
    "key":"#",
    "context": {
      "chatbotId": "a9928d68-92e6-4487-a2e8-8234fc9d1f48",
      "customData": {
        "name":"Kart",
        "email":"kart@yahoo.com",
        "phone":"123-4355-212",
      }
    }
  }' -X POST https://domain.comm100.com/api/v3/bot/sessions/f9928d68-92e6-4487-a2e8-8234fc9d1f48:submitIVRKey
```
Response
```Json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {    
    "channel":"IVR",
    "id": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
    "context": {
      "chatbotId": "a9928d68-92e6-4487-a2e8-8234fc9d1f48",
      "currentIntentId": "8d6892e6-92e6-4487-a2e8-92e68d6892e6",
      "customData": {
        "name":"Kart",
        "email":"kart@yahoo.com",
        "phone":"123-4355-212",
      }
    },
    "message":{
      "id":"d3f5b968-ad51-42af-b759-64c0afc40b84",
      "visitorQuestion":"2",
      "type":"highConfidenceAnswer",
      "content":{
        "intentId": "7534fdsca-92e6-4487-a2e8-92e68d6892e6",
        "intentName": "buy nbn",
        "score": 89.25,  
        "responses":[
          {
            "type":"text",
            "content": {
              "text":"Hi, I'm Peely, I'm glad to help you.",
              "audio":"UklGRrj2AQBXQVZFZm10IBAAAAABAAEAwF0AAIC7AAACABAAZGF0YZT2AQA..."
            }
          },
          {
            "type":"text",
            "content": {
              "text":"You can ask any questions. If you want to know what I can help with, you can say Menu or Options",
              "audio":"UklGRrj2AQBXQVZFZm10IBAAAAABAAEAwF0AAIC7AAACABAAZGF0YZT2AQA..."
            }
          }
        ]
      }
    }    
  }
```

### Rate the bot answer as helpful or not helpful

  `POST /api/v3/bot/sessions/{sessionId}:rate`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `sessionId` | Guid | yes  |  id of the chat or conversation |

Request body

The request body contains data with the follow structure:

  | Name | Type | Required  | Default | Description |    
  | - | - | :-: | :-: |  - | 
  | `channel` | string  | yes | | eg: `Live Chat`, `Facebook Messenger`, `Twitter Direct Message`, `WeChat`, `WhatsApp`, `SMS` |
  | `chatbotMessageId` | Guid  | yes | | the id of the [ChatbotMessage](#ChatbotMessage-object) |
  | `type` | string  | yes  | | `helpful` or `notHelpful` |
  | `context` | [ChatbotSessionContext](#ChatbotSessionContext-Object) Object  | yes  |  |

  example:
```Json 
  {
    "channel":"Live Chat",
    "chatbotMessageId":"4487fc9d-92e6-4487-a2e8-92e68d6892e6",
    "type": "notHelpful",
    "context": {
      "chatbotId": "a9928d68-92e6-4487-a2e8-8234fc9d1f48",
      "customData": {
        "name":"Kart",
        "email":"kart@yahoo.com",
        "phone":"123-4355-212",
      }
    }
  }
```
#### Response
the response is: [ChatbotSession](#ChatbotSession-Object) Object

#### Example
- Rate the bot as not helpful

  Using curl
```
curl -H "Content-Type: application/json" -d '{
    "channel":"Live Chat",
    "chatbotMessageId":"4487fc9d-92e6-4487-a2e8-92e68d6892e6",
    "type": "notHelpful",
    "context": {
      "chatbotId": "a9928d68-92e6-4487-a2e8-8234fc9d1f48",
      "customData": {
        "name":"Kart",
        "email":"kart@yahoo.com",
        "phone":"123-4355-212",
      }
    }
  }' -X POST https://domain.comm100.com/api/v3/bot/sessions/f9928d68-92e6-4487-a2e8-8234fc9d1f48:rate
```
  Response
```Json
  HTTP/1.1 200 OK
  Content-Type:  application/json
  {    
    "channel":"Live Chat",
    "id": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
    "context": {
      "chatbotId": "a9928d68-92e6-4487-a2e8-8234fc9d1f48",
      "customData": {
        "name":"Kart",
        "email":"kart@yahoo.com",
        "phone":"123-4355-212",
      }
    },
    "message":{
      "id":"d3f5b968-ad51-42af-b759-64c0afc40b84",
      "visitorQuestion":"",
      "type":"notHelpfulMessage",
      "content":{
        "messageWhenNotHelpful":"I am sorry that this doesn't answer your question. Please click on following button to connect to an agent.",
        "ifIncludeContactAgentOptionWhenNotHelpful": true,
      },
      "smartTriggerActions":[
        {
          "type":"transfer", 
          "isEnabled": true,
          "targetType": "department",
          "selectedDepartments": ["sadwe21d-92e6-4487-a2e8-92e68d6892e6"] 
        }
      ]
    }    
  }  
```

- Rate the bot as helpful

  Using curl
```
curl -H "Content-Type: application/json" -d '{
    "channel":"Live Chat",
    "chatbotMessageId":"4487fc9d-92e6-4487-a2e8-92e68d6892e6",
    "type": "helpful",
    "context": {
      "chatbotId": "a9928d68-92e6-4487-a2e8-8234fc9d1f48",
      "customData": {
        "name":"Kart",
        "email":"kart@yahoo.com",
        "phone":"123-4355-212",
      }
    }
  }' -X POST https://domain.comm100.com/api/v3/bot/sessions/1487fc9d-92e6-4487-a2e8-92e68d6892e6:rate
```
  Response
```Json
HTTP/1.1 200 OK
  Content-Type:  application/json
  {    
    "channel":"Live Chat",
    "id": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
    "context": {
      "chatbotId": "a9928d68-92e6-4487-a2e8-8234fc9d1f48",
      "customData": {
        "name":"Kart",
        "email":"kart@yahoo.com",
        "phone":"123-4355-212",
      }
    }       
  }
```


# Agent Assist Suggestion
  + `POST /api/v3/agentAssist/questionSuggestions` -[Query question suggestions by agent assist](#query-question-suggestions-by-agent-assist)

## Agent Assist Suggestion Related Object Json Format

### QuestionSuggestion

  QuestionSuggestion is represented as simple flat JSON objects with the following keys:  

  | Name | Type |  Default | Description |
  | - | - | :-: | - |
  | `id` | string  |  | the unique id of the question |
  | `question` | string  |  | the question visitor asked. |
  | `ifMatch` | bool  | false | if the suggestion score greater than highConfidenceScore then true, otherwise false |
  | `suggestions` | [Suggestion](#suggestion)[] |  | array of [Suggestion](#suggestion) Object |

### Suggestion

  Suggestion is represented as simple flat JSON objects with the following keys:  

  | Name | Type |  Default | Description |
  | - | - | :-: |  - |
  | `type` | string  |  | enum value, `publicCannedMessage`,`KBArticle`, `chatbotIntent` |
  | `content` | object  |  |suggestion's content.<br/>when type is publicCannedMessage, it represents [CannedMessageSuggestionContent](#canned-message-suggestion-content);<br/>when type is KBArticle ,it represents [KBArticleSuggestionContent](#kb-Article-suggestion-content);<br/>when type is chatbotIntent, it represents [ChatbotIntentSuggestionContent](#chatbot-Intent-suggestion-content). |
  | `score` | float  |  0 |the score of the suggestion |
 
### Canned Message Suggestion Content
  Canned Message Suggestion Content is represented as simple flat JSON objects with the following keys:  

  | Name | Type |  Default | Description |    
  | - | - | :-: | - | 
  | `id` | Guid  |  |id of the Canned Message |
  | `name` | string  |  |title of the Canned Message |
  | `content` | string  |  |the content of the Canned Message |

### KB Article Suggestion Content
  KB Article Suggestion Content is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Default | Description |    
  | - | - | :-: |  - | 
  | `id` | Guid  |  |id of the Knowledge Base article |
  | `title` | string  ||title of the article |
  | `content` | string  |  |the content of the article |
  | `url` | string  |  |the URL of the article |
  | `textBeforeKBArticle` | string  |  | the message which usually works as guidance for visitors before a knowledge base article link |

### Chatbot Intent Suggestion Content
  Chatbot Intent Suggestion Content is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Default |Description |    
  | - | - | :-: | - | 
  | `id` | Guid  |  |id of the intent |
  | `name` | string  |  |name of the intent |
  | `content` | string  |  |the content of the intent answers |


## Agent Assist Suggestion Endpoints
### Query question suggestions by agent assist

  `POST /api/v3/agentAssist/questionSuggestions`
 
#### Parameters

Request body

The request body contains data with the list of the follow structure:

  | Name | Type | Required | Default | Description |    
  | - | - | :-: | :-: | - | 
  | `id` | string  | yes | | the unique id of the question  |
  | `question` | string  | yes | | the question visitor asked. |
  | `campaignId` | Guid | no | | the campaign id |


example:
  ```json
  [ 
    {
      "id": "w124sad2-92e6-4487-a2e8-8234fc9d1f48",
      "question": "how to use livechat?",
      "campaignId": "w124sad2-92e6-4487-a2e8-8234fc9d1f48"
    },
    {
      "id": "fff4sad2-92e6-4487-a2e8-8234fc9d1f48",
      "question": "what is comm100 livechat about?",
      "campaignId": "w124sad2-92e6-4487-a2e8-8234fc9d1f48"
    }
  ]
```
#### Response    

 - the response is: list of [QuestionSuggestion](#questionSuggestion) Objects

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '[ 
    {
      "id": "w124sad2-92e6-4487-a2e8-8234fc9d1f48",
      "question": "how to use livechat?",
      "campaignId": "w124sad2-92e6-4487-a2e8-8234fc9d1f48"
    },
    {
      "id": "fff4sad2-92e6-4487-a2e8-8234fc9d1f48",
      "question": "what is comm100 livechat about?",
      "campaignId": "w124sad2-92e6-4487-a2e8-8234fc9d1f48"
    }
  ]' -X POST https://domain.comm100.com/api/v3/agentAssist/questionSuggestions
```
Response
```json
HTTP/1.1 200 OK
Content-Type:  application/json

[
  {
    "id": "w124sad2-92e6-4487-a2e8-8234fc9d1f48",
    "question": "how to use livechat?",
    "ifMatch": false,
    "suggestions": [
      {
        "type": "intent",
        "content": {
          "id": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
          "name": "comm100 livechat",
          "content":""
        },
        "score": 10
      }
    ]
  },
  {
    "id": "fff4sad2-92e6-4487-a2e8-8234fc9d1f48",
    "question": "what is comm100 livechat about?",
    "ifMatch": true,
    "suggestions": [
      {
        "type": "intent",
        "content": {
          "id": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
          "name": "comm100 livechat",
          "content":""
        },
        "score": 88.5
      }
    ]
  }
]
```
