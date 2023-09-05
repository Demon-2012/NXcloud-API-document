**Brief Description:**

- Query CDR (Call Detail Record) by order ID.
- Each approval request can only call this interface once per second. Excessive calls will be rate-limited and return "appkey access rate limit".
- Only allows querying CDR within the last 15 days. Please query in a timely manner and store the data on your end.

**Request Method:**
- URL: `https://api.nxcloud.com/api/voiceSms/getSipCdrByOrderid`
- Method: `POST`
- Content-Type: `application/json`

**Request Parameter Description:**

|Parameter|Required|Type|Description|
|:----    |:---|:----- |-----   |
|orderid|Yes|string|Order ID, a unique value provided by the user; multiple orders can be queried, separated by commas, e.g., orderid=1000001,1000002... Up to 20 orders can be queried at a time.|
|appkey|Yes|string|App key of any agent approval request|
|secretkey|Yes|string|Secret key of any agent approval request|

**Request Example:**
```shell
curl --location --request POST 'https://api.nxcloud.com/api/voiceSms/getSipCdrByOrderid' \
--header 'Content-Type: application/json' \
--data-raw '{
    "orderid": 10001,
    "appkey":"asdf",
    "secretkey":"qwer"
}'
```

**Response Example:**

``` 
**Successful Response**
{
    "code": "0",
     "row": [
	 {
	 "phone": "81314382782",
	 "direction": "0",
	 "hangup_cause": "NORMAL_CLEARING",
	 "answer_time": "2019-01-25 12:41:57",
	 "country_code": "62",
	 "id": 636597,
	 "sipid": 1055014,
	 "duration": 0,
	 "username": "6282215699804",
	 "end_time": "2019-01-25 12:42:26",
	 "effective_called_number": "626281314382782",
	 "start_time": "2019-01-25 12:42:26",
	 "orderid": "1000001",
	 "record_url": "http://wss.wanlaowo.com/record/c8b4cc48.mp3",
	 "show_phone": "6282215699804"
	 },
	 {
	 "phone": "878828666",
	 "direction": "0",
	 "hangup_cause": "NORMAL_CLEARING",
	 "answer_time": "2019-01-25 12:40:42",
	 "country_code": "62",
	 "id": 636600,
	 "sipid": 1055015,
	 "duration": 0,
	 "username": "6282215699803",
	 "end_time": "2019-01-25 12:42:29",
	 "effective_called_number": "626287882866266",
	 "start_time": "2019-01-25 12:42:29",
	 "orderid": "10000002",
	 "record_url": null,
	 "show_phone": "6282215699803"
	 }
        ]
    }
```
``` 
**Failed Response**
  {
    "code": "1",
    "info": "params invalid"
  }
```
 
 **Response Parameter Description:**

|Parameter|Required|Type|Description|
|:----    |:---|:----- |-----   |
|sipid|Yes|string|SIP ID, can be ignored|
|id|Yes|string|Call record ID, guaranteed to be unique, can be used to compare if the data is duplicated|
|username |Yes  |string |Phone username  |
|duration |Yes |string |Call duration   |
|phone|Yes|string|Original called number|
|start_time  |Yes | string|Call start time |
|end_time|Yes|string|Call end time|
|orderid|Yes|string|Order ID|
|show_phone|Yes|string|Call display number|
|record_url |Yes  |number |Recording file. If the call duration is 0, there is no recording file |
|answer_time|Yes|string|Call answer time|
|direction|Yes|string|Call direction. 0 for incoming, 1 for outgoing |
|effective_called_number|Yes|string|Normalized called number |
|hangup_cause |Yes  |string |Call hangup reason |
 
 
 
 


 Hangup Cause                     | Description                                                  
 --------------------------------| ------------------------------------------------------------
 *UNSPECIFIED*                    | This is usually given by the router when none of the other codes apply. This cause usually occurs in the same type of situations as cause 1, cause 88, and cause 100. 
 *UNALLOCATED_NUMBER*             | This cause indicates that the called party cannot be reached because, although the called party number is in a valid format, it is not currently allocated (assigned). 
 *NO_ROUTE_TRANSIT_NET*           | This cause indicates that the equipment sending this cause has received a request to route the call through a particular transit network, which it does not recognize. The equipment sending this cause does not recognize the transit network either because the transit network does not exist or because that particular transit network, while it does exist, does not serve the equipment which is sending this cause. 
 *NO_ROUTE_DESTINATION*           | This cause indicates that the called party cannot be reached because the network through which the call has been routed does not serve the destination desired. This cause is supported on a network dependent basis. 
 *CHANNEL_UNACCEPTABLE*           | This cause indicates that the channel most recently identified is not acceptable to the sending entity for use in this call. 
 *CALL_AWARDED_DELIVERED*         | This cause indicates that the user has been awarded the incoming call, and that the incoming call is being connected to a channel already established to that user for similar calls (e.g. packet-mode x.25 virtual calls). 
 *NORMAL_CLEARING*                | This cause indicates that the call is being cleared because one of the users involved in the call has requested that the call be cleared. Under normal situations, the source of this cause is not the network. 
 *USER_BUSY*                      | This cause is used to indicate that the called party is unable to accept another call because the user busy condition has been encountered. This cause value may be generated by the called user or by the network. In the case of user determined user busy it is noted that the user equipment is compatible with the call. 
 *NO_USER_RESPONSE*               | This cause is used when a called party does not respond to a call establishment message with either an alerting or connect indication within the prescribed period of time allocated. 
 *NO_ANSWER*                      | This cause is used when the called party has been alerted but does not respond with a connect indication within a prescribed period of time. Note - This cause is not necessarily generated by Q.931 procedures but may be generated by internal network timers. 
 *SUBSCRIBER_ABSENT*              | This cause value is used when a mobile station has logged off, radio contact is not obtained with a mobile station or if a personal telecommunication user is temporarily not addressable at any user-network interface. Sofia SIP will normally raise USER_NOT_REGISTERED in such situations. 
 *CALL_REJECTED*                  | This cause indicates that the equipment sending this cause does not wish to accept this call, although it could have accepted the call because the equipment sending this cause is neither busy nor incompatible. The network may also generate this cause, indicating that the call was cleared due to a supplementary service constraint. The diagnostic field may contain additional information about the supplementary service and reason for rejection. 
 *NUMBER_CHANGED*                 | This cause is returned to a calling party when the called party number indicated by the calling party is no longer assigned, The new called party number may optionally be included in the diagnostic field. If a network does not support this cause, cause no: 1, unallocated (unassigned) number shall be used. 
 *REDIRECTION_TO_NEW_DESTINATION* | This cause is used by a general ISUP protocol mechanism that can be invoked by an exchange that decides that the call should be set-up to a different called number. Such an exchange can invoke a redirection mechanism, by use of this cause value, to request a preceding exchange involved in the call to route the call to the new number. 
 *EXCHANGE_ROUTING_ERROR*         | This cause indicates that the destination indicated by the user cannot be reached, because an intermediate exchange has released the call due to reaching a limit in executing the hop counter procedure. This cause is generated by an intermediate node, which when decrementing the hop counter value, gives the result 0. 
 *DESTINATION_OUT_OF_ORDER*       | This cause indicates that the destination indicated by the user cannot be reached because the interface to the destination is not functioning correctly. The term "not functioning correctly" indicates that a signal message was unable to be delivered to the remote party; e.g. a physical layer or data link layer failure at the remote party, or user equipment off-line. 
 *INVALID_NUMBER_FORMAT*          | This cause indicates that the called party cannot be reached because the called party number is not in a valid format or is not complete. 
 *FACILITY_REJECTED*              | This cause is returned when a supplementary service requested by the user cannot be provide by the network. 
*RESPONSE_TO_STATUS_ENQUIRY*     | This cause is included in the STATUS message when the reason for generating the STATUS message was the prior receipt of a STATUS INQUIRY. 
 *NORMAL_UNSPECIFIED*             | This cause is used to report a normal event only when no other cause in the normal class applies. 
 *NORMAL_CIRCUIT_CONGESTION*      | This cause indicates that there is no appropriate circuit/channel presently available to handle the call. 
 *NETWORK_OUT_OF_ORDER*           | This cause indicates that the network is not functioning correctly and that the condition is likely to last a relatively long period of time e.g. immediately re-attempting the call is not likely to be successful. 
 *NORMAL_TEMPORARY_FAILURE*       | This cause indicates that the network is not functioning correctly and that the condition is not likely to last a long period of time; e.g. the user may wish to try another call attempt almost immediately. 
 *SWITCH_CONGESTION*              | This cause indicates that the switching equipment generating this cause is experiencing a period of high traffic. 
 *ACCESS_INFO_DISCARDED*          | This cause indicates that the network could not deliver access information to the remote user as requested, i.e. user-to-user information, low layer compatibility, high layer compatibility or sub-address as indicated in the diagnostic. It is noted that the particular type of access information discarded is optionally included in the diagnostic. 
 *REQUESTED_CHAN_UNAVAIL*         | This cause is returned when the other side of the interface cannot provide the circuit or channel indicated by the requesting entity. 
 *FACILITY_NOT_SUBSCRIBED*        | This cause indicates that the user has requested a supplementary service, which is available, but the user is not authorized to use. 
 *OUTGOING_CALL_BARRED*           | This cause indicates that although the calling party is a member of the CUG for the outgoing CUG call, outgoing calls are not allowed for this member of the CUG. 
 *INCOMING_CALL_BARRED*           | This cause indicates that although the called party is a member of the CUG for the incoming CUG call, incoming calls are not allowed to this member of the CUG. 
 *BEARERCAPABILITY_NOTAUTH*       | This cause indicates that the user has requested a bearer capability that is implemented by the equipment which generated this cause but the user is not authorized to use. 
 *BEARERCAPABILITY_NOTAVAIL*      | This cause indicates that the user has requested a bearer capability which is implemented by the equipment which generated this cause but which is not available at this time. 
 *SERVICE_UNAVAILABLE*            | This cause is used to report a service or option not available event only when no other cause in the service or option not available class applies. 
 *BEARERCAPABILITY_NOTIMPL*       | This cause indicates that the equipment sending this cause does not support the bearer capability requested. 
 *CHAN_NOT_IMPLEMENTED*           | This cause indicates that the equipment sending this cause does not support the channel type requested 
 *FACILITY_NOT_IMPLEMENTED*       | This cause indicates that the equipment sending this cause does not support the requested supplementary services. 
 *SERVICE_NOT_IMPLEMENTED*        | This cause is used to report a service or option not implemented event only when no other cause in the service or option not implemented class applies. 
 *INVALID_CALL_REFERENCE*         | This cause indicates that the equipment sending this cause has received a message with a call reference which is not currently in use on the user-network interface. 
 *INCOMPATIBLE_DESTINATION*       | This cause indicates that the equipment sending this cause has received a request to establish a call which has low layer compatibility, high layer compatibility or other compatibility attributes (e.g. data rate) which cannot be accommodated. 
 *INVALID_MSG_UNSPECIFIED*        | This cause is used to report an invalid message event only when no other cause in the invalid message class applies. 
 *MANDATORY_IE_MISSING*           | This cause indicates that the equipment sending this cause has received a message which is missing an information element which must be present in the message before that message can be processed. 
 *MESSAGE_TYPE_NONEXIST*          | This cause indicates that the equipment sending this cause has received a message with a message type it does not recognize either because this is a message not defined of defined but not implemented by the equipment sending this cause. 
 *WRONG_MESSAGE*                  | This cause indicates that the equipment sending this cause has received a message such that the procedures do not indicate that this is a permissible message to receive while in the call state, or a STATUS message was received indicating an incompatible call state. 
 *IE_NONEXIST*                    |This cause indicates that the equipment sending this cause has received a message which includes information element(s)/parameter(s) not recognized because the information element(s)/parameter name(s) are not defined or are defined but not implemented by the equipment sending the cause. This cause indicates that the information element(s)/parameter(s) were discarded. However, the information element is not required to be present in the message in order for the equipment sending the cause to process the message. 
 *INVALID_IE_CONTENTS*            | This cause indicates that the equipment sending this cause has received and information element which it has implemented; however, one or more fields in the I.E. are coded in such a way which has not been implemented by the equipment sending this cause. 
 *WRONG_CALL_STATE*               | This cause indicates that a message has been received which is incompatible with the call state. 
 *RECOVERY_ON_TIMER_EXPIRE*       | This cause indicates that a procedure has been initiated by the expiration of a timer in association with error handling procedures. This is often associated with NAT problems. Ensure that "NAT Mapping Enable" is turned on in your ATA. If it is not NAT related it can sometimes be provider related, make sure to ensure another outbound provider does not solve the problem.FreeSWITCH also returns this when the remote party sends a 408 for call expired. 
 *MANDATORY_IE_LENGTH_ERROR*      |This cause indicates that the equipment sending this cause has received a message which includes parameters not recognized because the parameters are not defined or are defined but not implemented by the equipment sending this cause. The cause indicates that the parameter(s) were ignored. In addition, if the equipment sending this cause is an intermediate point, then this cause indicates that the parameter(s) were passed unchanged. 
 *PROTOCOL_ERROR*                 | This cause is used to report a protocol error event only when no other cause in the protocol error class applies. 
 *INTERWORKING*                   | This cause indicates that an interworking call (usually a call to SW56 service) has ended. 
 *ORIGINATOR_CANCEL*              |                                                              
 *CRASH*                          |                                                              
 *SYSTEM_SHUTDOWN*                |                                                              
 *LOSE_RACE*                      |                                                              
 *MANAGER_REQUEST*                | This cause is used when you send an api command to make it hangup. For example uuid_kill <uuid> 
 *BLIND_TRANSFER*                 |                                                              
 *ATTENDED_TRANSFER*              |                                                              
 *ALLOTTED_TIMEOUT*               | This cause means that the server canceled the call because the destination channel took too long to answer. 
 *USER_CHALLENGE*                 |                                                              
 *MEDIA_TIMEOUT*                  |                                                              
 *PICKED_OFF*                     | This cause means the call was picked up by intercepting it from another extension (i.e. dialing **ext_number from another extension). 
 *USER_NOT_REGISTERED*            | This means you tried to originate a call to a SIP user who forgot to register.  
 *GATEWAY_DOWN*                   | Gateway is down (not answering on OPTIONS or SUBSCRIBE)      
