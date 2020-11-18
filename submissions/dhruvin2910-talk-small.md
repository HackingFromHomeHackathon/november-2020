## Talk Small

### Preface:

Due to recent events (COVID-19), everyone started working remotely, completely.
Effective ways to communicate with your team while working becomes not just
*essential* but **necessary**.

As a developer, I spend majority of my day working inside my IDE. It's a
software with which I'm quite fluent. I think it's true for many developers.
With the shift in how we work, I think our tools need an upgrade as well.
After all, we are as efficient as our tools.

### Idea: Talk Small 

A Push to Talk (PTT) client, built on top of Jitsi, right inside
[Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=dhruvin-dev.talk-small).

Talk Small's purpose is to provide a persistent communication channel.
You use it only when you want to broadcast/reply.
Like a [HAM Radio](https://en.wikipedia.org/wiki/Amateur_radio), but for VSCode. 
You can be free in your creative space. No more muting yourself after speaking.
Or worse, forgetting muting yourself even after speaking.

If you played multiplayer games, you may have used in-game audio chat solution.
Or maybe discord. It's a game changer! Haha. Please don't cut my points for this.

Talk small is similar to it. You host/join a room. But your audio is sent only
while you hold the spacebar key or the microphone button. Unlike an open-mic.

There are some alternatives like
[Live Share by Microsoft](https://docs.microsoft.com/en-us/visualstudio/liveshare/)
and [Code With Me by JetBrains](https://blog.jetbrains.com/blog/2020/09/28/code-with-me-eap/)
that are built mainly for active sessions.

### Use cases:

1. Push to Talk can be helpful in time-bound collaborative team tasks, like
remote hackathons, where all team members are communicating with each-other
quite often.

1. As remote stand-up meeting client. Since stand-up meetings are usually short,
and you chime in only when needed, you can do it right from your editor.

1. As @ThisIsJohnBrown suggested during the hackathon, it can be that "war room"
during releases for easy communication, which is basically just everyone sitting
muted on a call.

### Approach:

Key points I kept in mind while I was developing

1. Try to be minimal if not invisible:
    1. I wanted the extension to be invisible. Driven only by keyboard shortcuts,
    menus, and native inputs. But VSCode has limitations. No fine grain events
    for UI elements, required to implement "Push" in PTT.
    1. Hence, it has a minimal UI. Modern HAM radio look. (Yep! That's what I'm
    going with.) Only parts that are necessary for a participant are shown.

1. Try to integrate with VSCode as much as possible:
    1. VSCode has extensive theme support. I wanted to make sure the webview I
    create must fit inside your VSCode with your theme.
    1. I used appropriate extension points whenever possible. Display Name can
    be set via VSCode configuration, all user inputs are done through VSCode.
    1. Native notification and error message support. Buttons and commands in
    VSCode are shown or hidden according to conference call's state.
    1. Saving and restoring last joined room's name. And more.

1. Try to preserve privacy and enforce security:
    1. Rooms created from VSCode must have a password set. I don't want
    zoombombing happen to your calls. Especially when it's related to your work.
    1. No open Mic. Speaking is deliberate action, by design.

1. Try to keep the code as readable/auditable as possible

1. Try embracing modern toolchains

### Links:

- [Project](https://github.com/dhruvin2910/talk-small)
- [Issues](https://github.com/dhruvin2910/talk-small/issues)
- [Screenshots](https://github.com/dhruvin2910/talk-small/blob/master/README.md#screenshots)
