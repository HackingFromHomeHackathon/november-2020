## mattermost-jitsi-proxy

mattermost-jitsi-proxy is a set of services deployed on as docker containers to connect a Mattermost channel to a Jitsi chat box.

## link to the repository
[click here](https://github.com/amirphl/mattermost-jitsi-proxy)

## perquisites
you need to have a running jitsi meet with at least one Prosody, Jicofo, and Videobridge + Nginx

# introduction
### problem statement and use case
Large conferences with hundreds of participants are usually unstable and too noisy because of the noise of participant's microphone,
 also it is not always needed to add such a number of participants in a conference because most of them
do not share video and audio, also commuting of users are disruptive, so it seems it's better to separate environments of participants
who are willing to send audio or video from those who aren't, but there're two problems here, how participants can see the videos and listen to audios of a conference if they're not in the room?
How to send messages and receive messages form the conference?
So there are two problems here:
1- How do participants send and receive multimedia to and from a conference?
2- How to send and receive messages?
For the first problem, seems live stream is a good solution, for example, participants watch the live stream on youtube,
 but for the second problem, a solution is designed and implemented: **mattermost-jitsi-proxy**
With mattermost-jitsi-proxy, it is possible to send every messages of a channel to Jitsi chat box and vice versa.
In this case, participants who are not willing to share audio and video, join a public channel in Mattermost and the rest join the Jitsi conference, so in this manner, they can send messages to each other, ask questions and receives answers beside of
watching youtube lives stream.

## approach to design and implement such a system:
To solve the problem,  a second set of services are designed and implemented to connect a Mattermost channel to a Jitsi chat box.
These services are:
- **apis service**: a module (**mod_mattermost_proxy.lua**) is designed and implemented and added to Prosody so that the Prosody can send MUC (multi-user chat) messages (not all of them, only those which have a specific structure)
to another service called **apis services**. This service is responsible for getting messages for Prosody and send them to Mattermost via Mattermost api,
also for connecting each chat box to a channel, it requests another services called **websocket server** to spawn a long running process and listen for the events in the channel and send the events to Prosody.
- **websocket server**: this service spawns long running websockets which are connected to Mattermost api endpoint
and subscribe for events. If a post event is received, this service will deliver it to anther module
called **xmpp client service**, then the module sends it to Prosody.
- **xmpp client service**: it receives posts created in a channel from **websocket server** then
sends them to Prosody and after, it will be delivered to the client.

### scenarios
- from the point of view of channel owner who wants to connect his channel to a conference chat box:
The owner sends his Mattermost **username**, **password**, **team name**, **channel name**, and **room address** to
`http://apis_service_ip:port/generate-token/` to get an **encrypted** token. (see Authentication section for more info and security issues)
the command to get a token: `curl -d '{"username":"your Mattermost username" , "password":"your Mattermost password", "team_id":"team name", "channel_id":"public channel name", "room_id":"room name"}' -H "Content-Type: application/json" -X POST http://<apis_service:port ex:localhost:8000>/generate-token/ -v`
Now the owner has to send the token to the room with `room_id` provided in previous `curl` command by typing below message
in the chat box:
`/login <token>`

If the credentials are correct, **all users** in the chat box can send message to the connected channel by typing 
command:
`/message <message>`
Otherwise the message will be broadcasted only in the chat box, so all the messages with structure `/message <message>`
will also be sent in the channel.
Also after successful login, new posts of channel will be sent to the chat box.

- from the point of view of a member in channel or chat box:
After successful login of owner, every messages of members in channel are also sent to chat box, Also all
messages of the form `/message <message>` in chat box is sent to channel too.

## architecture
[architecture](https://drive.google.com/file/d/1lgCk2kBptpfP9QCdLQuy1EbV7RnD7w7V/view?usp=sharing)

## authentication
