# Frequently asked questions
This page covers most popular faq's which are categorised into sections.

## Manual verifications FAQ's

- ##### What is a manual verification?
A verification type where an identification is reviewed by our staff members.

- ##### How manual verification is different from automatic verification?
Manual verification is being performed by our staff members while automatic verification is
being performed by our automated algorithms. 

- ##### How does manual verification work?
In our office we have manual reviewers that look at automatically verified identifications 
one more time. They ensure that there were no fraudulent actions in identification 
process and algorithms accurately read data from a document.  

- ##### When does a manual verification "kick in"?
By default every single automatically verified identification is reviewed once more 
by our manual reviewers. This behaviour can be altered by your custom needs.

- ##### How do I know when identification was verified manually/automatically?
After a finished identification process in iDenfy platform you will be notified via email
and/or a HTTP call to you custom API endpoint. By default you can expect one notification 
(if an identification is reviewed only manually) or two notifications (first one is from
automatic and the second one is from manual verifications). Manual verification notification
is always the last notification. 

- ##### Is it possible that after a manual verification photos can get changed or modified by a manual reviewer?
No. The only thing that might change is the data read from the document due to possible OCR reading inaccuracies.

## Identification status FAQ's

- ##### What does "SUSPECTED" mean and when is it triggered?
This status means that our algorithms have detected a possible fraudulent activity in
identification process e.g. printed document or a face from mobile screen, etc. In such case
identification is terminated and a notification is sent with overall status as "SUSPECTED". 

- ##### What does "AUTO_UNVERIFIABLE" mean and when is it triggered?
This status means that the identification can not be reviewed automatically. Some of most common scenarios when this 
status is triggered is when a user select "Other documents" to do an identification (may not be applicable to you) or explicitly asks for a manual review (may not be applicable to you).

- ##### What causes identification to be denied?
There are many reasons why an identification can be denied. There might be various cases
associated with document scanning e.g. could not locate a face in a document, could 
not read name/surname from the document, document is too blurry, etc. Also, there might
be various cases associated with face detection and matching e.g. selfie face and 
document face look too different. Furthermore, in case LID or AML is enabled an identification could be denied because
the document used was registered as lost or a person is in PEP sanctions list.

- ##### When identification is considered approved?
It is considered approved when document and face analysis both succeed.
Document analysis: data from a document was read successfully and matched 
data provided when generating token. Face analysis: selfie face and document face
both match. Also, in case LID or AML is enabled a person has a valid document and is 
not in PEP sanctions list.


## Identification flow FAQ's

- ##### I see that a user has done a second identification even though the previous one was successful. Why is he allowed to do further identifications?
Because iDenfy platform does not track individual people that come to identify themselves.
iDenfy tracks only identifications and each identification has a unique number. 
Therefore you should ensure on your side that a client is not allowed to do 
an additional identification after a successful one. Also, iDenfy recommends 
restricting token generation for user if a previous one is not yet expired. 

- ##### When identification process is complete?
Identification process by default has 2 attempts. If You tried to identify yourself, and all 2 attempts in a row were unsuccessful, your identification process is complete (unsuccessfully). If You get successful identification per 2 attempts, your identification process is complete (successfully). If your session time exceeds, your identification process is complete (unsuccessfully). Sometimes users can interrupt the identification process by closing the browser window, in this case the identification process is still not complete. It completes when session time expires. So, our manual reviewer team can’t review identification immediately because session time hasn't expired and identification hasn't appeared in our system.
 

## Generating token FAQ's

- ##### What is the difference between expiryTime and sessionLength parameters? And what do they do?
The **expiryTime** parameter defines how long the generated token is going to live.
For example, if token was generated with expiry time of 3600 (1 hour) - 
a client can start his identification process any time withing that 1 hour.
After an hour is passed, a token will no longer be valid and and a client
will see an internal “session expired” page.
However **sessionLength** determines how long a client can stay in identification platform.
The **sessionLength** parameter takes effect only when a client visits 
the identification platform.
For example, if token was generated with session length of 600 (10 minutes)
a client has 10 minutes to identify himself (take photos of documents and his face)
in the platform. After 10 minutes a client will see an internal “session expired” page.

- ##### What if my client’s name/surname contains non-Latin characters?
We accept any type of characters (Latin and non-Latin).

## Webhook callback FAQ's

- ##### I am not receiving a callback. Why?
Please check the [Callback troubleshooting](https://github.com/idenfy/Documentation/blob/master/pages/ResultCallback.md#callback-troubleshooting) section. 

- ##### How do I differentiate which (manual or automatic) verification a callback represents?
Within received callback look for 'status' entry.
If `autoDocument` with `autoFace` fields are not empty and 
`manualDocument` with `manualFace` field are empty - it means the callback represents 
automatic verification. If `manualDocument` with `manualFace` fields are not empty - 
it means the callback represents manual verification.

- ##### What happens if my provided webhook endpoint is not accessible temporary?
iDenfy API will repeat a call once. If both times there was an error a "failed callback"
state is associated with the identification. If user has successfully identified himself
and callback has failed, a user will see an information popup, where it states that 
identification succeeded but there was an issue saving data. Also, a user will be 
redirected to a failure page.

- ##### Do you repeat callback sending?
Yes. iDenfy API will repeat a call once (after 0.5 seconds) if the initial callback sending has failed. If the second callback fails - an associated identification is flaged with "callback failed" state.

- ##### How many callbacks to expect?
If your identifications are processed only automatically - just one - after processing is done. 
If your identifications are processed automatically and then reviewed manually - then in total two - one after an automatic processing and one after a manual verification.

## Camera issues FAQ's

- ##### Why your platform can not detect camera when using an iPhone with Chrome or Firefox web-browser?
Currently (as of 2019-05) apple does not allow accessing camera to any browser except Safari.

- ##### Why your platform can not detect camera on Chrome with iFrame integration?
When using an `iframe` tag, make sure to add an attribute `allow="camera"`. 
