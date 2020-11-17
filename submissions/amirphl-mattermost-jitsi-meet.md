## mattermost-jitsi-proxy

**mattermost-jitsi-proxy** is a set of services deployed on as docker containers to connect a Mattermost channel to a Jitsi chat box.

## link to the repository
[click here](https://github.com/amirphl/mattermost-jitsi-proxy)

## perquisites
you need to have a running Jitsi meet with at least one Prosody, Jicofo, and Videobridge + Nginx

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
The token is generated and encrypted by **apis service** and will be decrypted by too. No one has set of keys
(public and private keys) to generate the token, so no one can create a token except that service.
All tokens expire after 30 minutes, so you need to login again after 30 minutes from the first login to be able to
send message to the channel while in this case still messages from the channel are sent to chat box (TODO: I have 
to handle it too, after expiration, no message is allowed to pass from the channel to the chat box and vice versa).
Because room_id is hardcoded in the token (user has to enter the room_id to get the token), thus no one can connect his
 room to a channel with someone's else token.
Also no one can extract the content of token because no one has the key except the service. 

## setup
- setup Jitsi meet (Prosody, Jicofo, Jvb) on your development server
- install `python3`
- install python `requests` package (`pip3 install requests`)
- clone project form [here](https://github.com/amirphl/mattermost-jitsi-proxy) on your dev server
- copy `prosody/mod_mattermost_proxy.lua` to `prosody-plugins/` of prosody
- copy `prosody/send_message.py` to `prosody-plugins/` of prosody
- change `APIS_URL` variable in `send_message.py` and fill it with your server IP address
- add `mattermost_proxy` to `modules_enabled` section of your MUC config in Prosody config file
- restart Prosody
- add '*' to `ALLOWED_HOSTS` in `mattermost_proxy/settings.py`
- run `openssl genrsa -out key.pem 2048` to generate RSA private key
- run `openssl rsa -in key.pem -outform PEM -pubout -out public.pem` to generate RSA public key
- run `export SIGNING_KEY=`cat public.pem``
- run `export VERIFYING_KEY=`cat key.pem`
- run `sudo ufw allow 8000` to open port 8000/tcp so that users could get token
- run `cp .env.example .env`
- now fill `.env` file with appropriate values:
- **SECRET_KEY** : used as the Django secret key
- **DEBUG** : debug mode for Django
- **GUNICORN_WORKERS** : number of gunicorn workers
- **MATTERMOST_API_URL** : your server IP address (users connect to this IP to use Mattermost so it's better 
to use public IP so people can reach you). This is also IP address of Mattermost endpoint
- **XMPP_SERVICE_URL** : ex: wss://example.com/xmpp-websocket
- **XMPP_DOMAIN** : ex: example.com
- run `docker run --name mattermost-preview -d --publish 8065:8065 --add-host dockerhost:127.0.0.1 mattermost/mattermost-preview` to setup a Mattermost instance
- run `sudo ufw allow 8065`
- run `docker-compose up -d --build`
- to see logs, run `docker logs service_name -f`. fill service_name with a correct value (service names)
- go to `http://your IP address:8065` and create an account then create a team and a public channel
- run `curl -d '{"username":"your Mattermost username" , "password":"your Mattermost password", "team_id":"team name", "channel_id":"public channel name", "room_id":"room name"}' -H "Content-Type: application/json" -X POST http://<your IP ex: localhost:8000>/generate-token/ -v` to obtain a token
- now go to a Jitsi conference and in the chat box type: `/login <your token>`
- now in the chat box type: `/message hello`
- go to channel and you will see a `hello` message
- in the channel type `how are you?`
- go to Jitsi chat box and now you see a `how are you?` message
- note: an echo message shows that message is delivered successfully


## TODO
- better exception handling for all parts of code
- reuse websocket connections in **xmpp client service**
- handling messages which start by slash (/) in a channel (what happens in this case?)
- use other Mattermost APIs and integrate with them (ex: kicking out user from channel by API)
- optimize process termination in **websockets service** (also test right behaviour again)
- repetitive login commands cause additional overhead by terminating long running websocket process in **websocket server service**
and querying redis, .... somehow this action must be controlled but sometimes it's necessary, for example, 
when channel credentials is changed by user and use neet to login again
- distinguish between post message and reply (customization)
- using celery to send message from **websockets service** to **xmpp client service** to increase performance
- using celery to send message from **apis service** to **Mattermost** to increase performance
- using celery to initiates long running websocket connection from **websockets service** to
**Mattermost** to increase performance
- merge **xmpp client service** to **websockets service** and use python xmpp client library instead of
nodejs xmppjs library
- perform more control on requests to increase performance in *mod_mattermost_proxy.lua*
- implement logout method
- writing unit tests
- create html page for users to get a token and using nginx to serve it
- **deny path /api/v4/ of Mattermost for outsiders, only services are allowed to use it** 
- add version for requirements.txt

