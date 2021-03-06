  | Change Version | API Version | Change nots | Change Date | Author |
  | - | - | - | - | - |
  | 1.0 | v1 | Taskbot API V1 | 2020-12-10 | Light |


# Summary
  - Taskbot
    - [session](#session)  


# Session
  - `POST /v1/taskbot/taskbots/{taskbotId}/sessions` - [Create session](#create-session)
  - `POST /v1/taskbot/sessions/{sessionId}:triggerAction` - [Trigger Action](#trigger-action)
  - `POST /v1/taskbot/sessions/{sessionId}:endSession` - [End Session](#end-session)

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
  | `sessionId` | Guid  | | sessionId |
  | `taskbotId` | Guid  | | taskbotId |
  | `taskbotVersionId` | Guid  | | current session versionId of taskbot  |
  | `TaskbotTriggerRecordId` | Guid  | | triggerRecordId  |
  | `authentication` | string  | | authentication data |
  | `location` | string  | | the longitude and latitude of the location, e.g. "-39.900000,116.300000" |
  | `inputText` | string  | | inputText |
  | `integrationCalendlyId` | Guid  | | integrationCalendlyId |
  | `variables` | [NameValueCollection](#NameValue-object) |  | an array of [NameValue](#NameValue-object) objects |
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
  | `latestNextActionIds` | Guid[]  |  | record latest message can locate next action 
  | `latestpath` | string  |  | pre response path,like '1.2.3.1.2' |
  | `messages` | List<MessageData>  |  | MessageData  |
  
  MessageData Object is represented as simple flat JSON objects with the following keys: 
  |Name| Type| Default | Description     | 
  | - | - | :-: | - | 
  | `type` | string  |  | type of the response,including `taskbotSendMessage`,`taskbotQuickReply`、 `taskbotSendImage`、`taskbotSendVideo`、`taskbotSSOLoginButton`,`taskbotCollectLocation`, `taskbotCollectCompany`, `taskbotCollectEmail`, `taskbotCollectName`, `taskbotCollectPhoneNumber`, `taskbotCollectComment`,`taskbotCollectVariableData`,`taskbotBookMeeting`,`taskbotTransferChat`,`taskbotGotoTaskbot` |
  | `content` | object |  | response's content. when type is `taskbotSendMessage`, it represents [SendMessage](#SendMessage-object); when type is `taskbotQuickReply`,it represents [QuickReply](#QuickReply-object);when type is `taskbotSendImage`,it represents [SendImage](#SendImage-object);when type is `taskbotSendVideo`,it represents [SendVideo](#SendVideo-Object); when type is `taskbotSSOLoginButton`, it represents [SSOLoginButton](#SSOLoginButton-Object);when type is `taskbotCollectLocation`, it represents [CollectLocation](#CollectLocation-Object);when type is `taskbotCollectCompany`, it represents [CollectCompany](#CollectCompany-Object);when type is `taskbotCollectEmail`, it represents [CollectEmail](#CollectEmail-Object);when type is `taskbotCollectName`, it represents [CollectName](#CollectName-Object);when type is `taskbotCollectPhoneNumber`, it represents [CollectPhoneNumber](#CollectPhoneNumber-Object);when type is `taskbotCollectComment`, it represents [CollectComment](#CollectComment-Object);when type is `taskbotCollectVariableData`, it represents [CollectVariableData](#CollectVariableData-Object);when type is `taskbotBookMeeting`, it represents [BookMeeting](#BookMeeting-Object);when type is `taskbotTransferChat`, it represents [TransferChat](#TransferChat-Object);when type is `taskbotGotoTaskbot`,  it represents [GotoTaskbot](#GotoTaskbot-Object);|


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
  | `text` | strubg |  |   String (256). |  
  | `nextActionId` | guid | |  |
  | `order` | int | | Order Number|
  


### SendImage Object

  SendImage is represented as simple flat JSON objects with the following keys:  

  | Name | Type |  Default | Description |    
  | - | - | - | - | 
  | `typingDelay` | decimal |  |  float (0.0-10.0). Default: 1.0. The typing delay in seconds before this message is shown in chat window. Visitor can see bot is typing in chat window |  
  | `message` | string | | HTML Text.  |
  | `imageUrl` | string | | url  |
  | `nextActionId` | guid | | NextActionId |

###  SendVideo Object

  SendVideo is represented as simple flat JSON objects with the following keys:  

  | Name | Type |  Default | Description |    
  | - | - | - | - | 
  | `typingDelay` | decimal |  |  float (0.0-10.0). Default: 1.0. The typing delay in seconds before this message is shown in chat window. Visitor can see bot is typing in chat window |  
  | `message` | string | | HTML Text.  |
  | `videoUrl` | string | | url  |
  | `nextActionId` | guid | | NextActionId |

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


###  CollectCompany Object

   CollectCompany is represented as simple flat JSON objects with the following keys:  

  | Name | Type  | Default | Description |    
  | - | - | :-: | - | 
  | `typingDelay` | decimal |  |  float (0.0-10.0). Default: 1.0. The typing delay in seconds before this message is shown in chat window. Visitor can see bot is typing in chat window |  
  | `message` | string  |  | message of the sign in |
  | `nextActionId` | guid | | NextActionId |
  
  
###  CollectEmail Object

   CollectEmail is represented as simple flat JSON objects with the following keys:  

  | Name | Type  | Default | Description |    
  | - | - | :-: | - | 
  | `typingDelay` | decimal |  |  float (0.0-10.0). Default: 1.0. The typing delay in seconds before this message is shown in chat window. Visitor can see bot is typing in chat window |  
  | `message` | string  |  | message of the sign in |
  | `nextActionId` | guid | | NextActionId |


###  CollectName Object

   CollectName is represented as simple flat JSON objects with the following keys:  

  | Name | Type  | Default | Description |    
  | - | - | :-: | - | 
  | `typingDelay` | decimal |  |  float (0.0-10.0). Default: 1.0. The typing delay in seconds before this message is shown in chat window. Visitor can see bot is typing in chat window |  
  | `message` | string  |  | message of the sign in |
  | `nextActionId` | guid | | NextActionId |
  
  
###  CollectPhoneNumber Object

   CollectPhoneNumber is represented as simple flat JSON objects with the following keys:  

  | Name | Type  | Default | Description |    
  | - | - | :-: | - | 
  | `typingDelay` | decimal |  |  float (0.0-10.0). Default: 1.0. The typing delay in seconds before this message is shown in chat window. Visitor can see bot is typing in chat window |  
  | `message` | string  |  | message of the sign in |
  | `nextActionId` | guid | | NextActionId |
  
  
 ###  CollectComment Object

   CollectComment is represented as simple flat JSON objects with the following keys:  

  | Name | Type  | Default | Description |    
  | - | - | :-: | - | 
  | `typingDelay` | decimal |  |  float (0.0-10.0). Default: 1.0. The typing delay in seconds before this message is shown in chat window. Visitor can see bot is typing in chat window |  
  | `message` | string  |  | message of the sign in |
  | `nextActionId` | guid | | NextActionId |
  
  
###  CollectVariableData Object

   CollectVariableData is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Default | Description |    
  | - | - | :-: | - | 
  | `typingDelay` | decimal |  |  float (0.0-10.0). Default: 1.0. The typing delay in seconds before this message is shown in chat window. Visitor can see bot is typing in chat window |  
  | `message` | string  |  | message of the sign in |
  | `variableName` | string  |  | variableName |
  | `type` | string  |  | enums:`text`, `textArea`, `singleSelect`, `mutipleSelect`, `email`, `password`, `date`, `time`|
  | `options` | string  |  | variableName |
  | `nextActionId` | guid | | nextActionId |


###  BookMeeting Object
 BookMeeting is represented as simple flat json objects with the following keys:

|Name| Type| Default | Description     | 
| - | - | :-: | - | 
| `IntegrationCalendlyId` | guid  |  | Calendly Account. |
| `SchedulUrl` | string  |  | SchedulUrl |
| `successActionId` | guid  |  | Taskbot Action Id |
| `failedActionId` | guid  |  | Taskbot Action Id |


###  TransferChat Object
   TransferChat is represented as simple flat JSON objects with the following keys:

  | Name | Type | Default | Description |
  | - | - | - | - |
  | `transferType` | string | |enums:`transferToAgent`, `transferToDepartment`, `transferToChatbot`, `transferRouting Rules`.  |
  | `transferTo` | guid | | Agent, Department, Chatbot. Only available when Type is Transfer to Agent, Transfer to Department, Transfer to Chatbot.  |
  | `agentOfflineActionId` | guid | | Task Bot Action. The action to go to when visitor replies with any other message |
  
###  GotoTaskbot Object
   GotoTaskbot is represented as simple flat JSON objects with the following keys:

  | Name | Type | Default | Description |
  | - | - | - | - |
  | `taskbotId` | guid | | go to other taskbot|


## Endpoints

### Create session
  - `POST /v1/taskbot/taskbots/{taskbotId}/sessions`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `taskbotId` | Guid | yes  |  the unique id of the taskbot |  

Request body

The request body contains data with the follow structure:

  | Name | Type | Required | Default | Description |    
  | - | - | :-: | :-: | - | 
  | `sessionId` | Guid  | yes | |id of the session |
  | `triggerType` | string | yes | | enums:`preChat`, `agent`, `chatbot`, `taskbot`|
  | `triggerBy` | guid | yes  || agentId or chatbotId or taskbotId |
  | `context` | [TaskbotContext](#TaskbotContext-Object) Object  | yes  |  |context|

example:
```Json 
  {
    "sessionId": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
    "triggerType":"agent",
    "triggerBy":"d3f5b968-ad51-42af-b759-64c0afc40b84",
    "context": {   
    }
  }
```

#### Response
the response is: [TaskbotSession](#TaskbotSession-Object) Object


#### Example
Using curl
```
Response
```Json
  HTTP/1.1 200 OK
  Content-Type:  application/json
```Json 
  {    
    "sessionId": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
    "context": {
      "taskbotId": "c332456g-92e6-4487-a2e8-8234fc9dvx32",
	  "taskbotVersionId": "cxzx1233-92e6-2437-a2e8-8234432fdds",
	  "authentication":"xxx",
	  "location":"xxx",
      "variableValues": {
        "name":"Kart",
        "email":"kart@yahoo.com",
        "phone":"123-4355-212",
      },
	  latestMessage:{}
    },
    "message":{
      "id":"d3f5b968-ad51-42af-b759-64c0afc40b84",
      "visitorQuestion":"",
      "type":"sendMessage",
      "content":{
      }
    }
}
```


### Trigger Action
`POST /v1/taskbot/sessions/{sessionId}:triggerAction`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `sessionId` | Guid | yes  |  id of the chat or conversation |


Request body

The request body contains data with the follow structure: if the node is bookmeeting, the inputtext is EventUri + ";" +EventInviteeUri

  | Name | Type | Required | Default | Description |    
  | - | - | :-: | :-: | - | 
  | `authentication` | string | no  |  Authentication Token |
  | `location` | string | no  |  location |
  | `inputText` | string | no  |  user input or equal option. we should use this value to megex the best equal nextactionid and variable name, booking meeting eventuri;eventinviteerui |
  | `context` | [TaskbotContext](#TaskbotContext-Object) Object  | yes  |  |context|

example:
```Json 
  {
    "intentId":"8d6892e6-92e6-4487-a2e8-92e68d6892e6",
    "authentication": "xxxxxx",
	"context":""
  }
```

#### Response
the response is: [TaskbotSession](#TaskbotSession-Object) Object

Response
```Json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {    
      "sessionId": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
      "context": {
      "taskbotId": "c332456g-92e6-4487-a2e8-8234fc9dvx32",
	  "taskbotVersionId": "cxzx1233-92e6-2437-a2e8-8234432fdds",
	  "authentication":"xxx",
	  "location":"xxx",
      "variableValues": {
        "name":"Kart",
        "email":"kart@yahoo.com",
        "phone":"123-4355-212",
      },
	  "latestMessage":{}
    },
    "message":{
      "id":"d3f5b968-ad51-42af-b759-64c0afc40b84",
      "visitorQuestion":"",
      "type":"sendMessage",
      "content":{
      }
    }  
  }
```


### End Session
`POST /v1/taskbot/sessions/{sessionId}:endSession`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `sessionId` | Guid | yes  |  id of the chat or conversation |


Request body

The request body contains data with the follow structure:

  | Name | Type | Required | Default | Description |    
  | - | - | :-: | :-: | - | 
  | `endType` | string | yes ||  enums:`completed`,`stopByAgent`, `chatEnd`|
  | `taskbotId` | Guid | yes  |  id of the taskbot |
  | `context` | [TaskbotContext](#TaskbotContext-Object) Object  | yes  |  |context|

example:
```Json 
  {
      "chatbotId": "a9928d68-92e6-4487-a2e8-8234fc9d1f48",
      "endType": "stopByAgent",
  }
```

#### Response

