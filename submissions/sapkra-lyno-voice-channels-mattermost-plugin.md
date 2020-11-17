## Lyno Voice Channels for Mattermost

This plugin provides a direct integration of voice channels into Mattermost.
This is made possible by [lyno.io](https://lyno.io) which is using Jitsi as the base.

![screenshot](https://github.com/lynoapp/mattermost-plugin-lyno/blob/master/screenshot.png?raw=true)

### Features

- Automatic authentication
- Always see all users which are currently in which rooms, even if you are not in the same room
- Mute audio
- Show who is speaking
- Play a sound when someone joins or leaves a room

### Problems this plugins solves

In remote teams we often have a decrease in communication, visability of colleagues and team spirit. All the communication between meetings, like at the watercooler/coffee machine or even quickly asking a colleague next to you, is completely lost. These problems will be solved by providing virtual rooms.

A virtual room is like an open space office in the real world, you can see who is currently present, who is talking to whom and join a conversation. No need for a random call or scheduling an appointment just see who is there and talk immediately to your team with a single click.

### How to use

This plugin currently has to be installed via a plugin upload. You can download the latest release [here](https://github.com/lynoapp/mattermost-plugin-lyno/releases).

After installing the plugin ui should automatically appear above the channel list.

Requirements:
- The `SiteURL` has to be configured
- Server has to be reachable from the internet

### Contributing

[source](https://github.com/lynoapp/mattermost-plugin-lyno)

Contributions are very welcome. Please feels free to submit a PR/issue.
Unfortunetly it is currently not possible to compile our plugin because some internal libraries are not publicly available yet.
