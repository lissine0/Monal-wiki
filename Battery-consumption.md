# Battery consumption displayed by Apple

Normally, Apple freezes apps so that the can't run if they are in the background and not woken up by some special event (see below).
That makes it possible to *very roughly* estimate the battery consumption of an app by measuring the time the app is not frozen.
This does not come without some caveats. The biggest one is, that an app that's not frozen, but doing nothing (e.g. being idle) consumes virtually no power. Whereas an app doing heavy calculations consumes much more power.
Using CPU utilization to estimate the battery consumption (like Android does) would improve the situation significantly. 
<details>
<summary>Why do these two systems estimate the battery consumption that differently?</summary><br>
I think this is the case because both systems started very differently.<br>

On Apple's iOS apps initially weren't allowed to run in the background at all and Apple only gradually added some background modes like pushes that wake up the app or frequent update tasks. When virtually no background time is allowed for apps, estimating the battery consumption using just the time an app is running (whether idle or not), is just good enough.

On Android on the other hand, apps were initially allowed to run in the background for as long as they wanted and Google only gradually added more and more limitations (that's the reason Conversations, the XMPP client for Android has to show this "I'm running" notification on modern Android phones by the way).
Having everything run as often and as long as it wants (often just being idle and doing nothing) made the estimation of battery consumption using just the time an app was running much more inaccurate on Android. So Google tried to do a more sophisticated estimation based on the CPU utilization and other factors.

Nowadays both systems allow more or less the same amount of background time, but the battery estimation still stayed the same on iOS while ideally it should have been changed to match that of Android.

That said: estimating the battery consumption is hard and a really accurate estimate hast to based on more than just the CPU utilization or bandwidth of network traffic generated etc. There is no perfect solution, even on Android it still is an *estimate*, not the real consumption.
</details>

## But, why is Monal listed as one of the apps with highest battery consumption while others aren't?

**First of all, make sure to use a server having a CSI module active because that will reduce the amount of XMPP protocol related "messages" that actually generate a push to only those that are important (e.g. new incoming messages, pushes to remove notifications for messages read on another device, incoming calls etc.). This has a huge impact on battery consumption! See our [Considerations for XMPP server admins](https://github.com/monal-im/Monal/wiki/Considerations-for-XMPP-server-admins) for more details.**

Every message you receive (either in a 1:1 chat or in a group/channel) triggers a push notification to your device.
These push notifications can either just contain the message that should be displayed which would be visible to Apple's servers, or be only a wake-up signal for the app to connect to the XMPP server and retrieve the actual message.
As privacy focused app, Monal naturally does the latter.

Every of these wakeup pushes grants Monal 30 seconds of background time before iOS freezes the app again. In these 30 seconds Monal (tries) to connect to the XMPP server, log in using your credentials, retrieve all pending messages and disconnect again.

But since most of the time a second message follows suit after a few seconds, directly disconnecting after retrieving everything *currently* pending would just generate another push a few seconds later and Monal would have to do this connect-log-in-retrieve dance again.
That means more traffic and more CPU consumption. So Monal uses the full 30 seconds time-frame to wait for another message while just sitting idle and doing nothing. This virtually consumes no battery as opposed to the traffic generated and amount of CPU time consumed by doing this whole dance again (build the encrypted TLS channel, log in to the XMPP server, retrieve the pending messages).

*Unfortunately using the full 30 seconds makes Monal look very bad in Apple's battery consumption display while in reality it isn't.*

### Help wanted
My claims can be tested by checking and comparing the actual battery consumption (the change in total battery percentage) when using the phone with and without Monal. Ideally as an average over, say, 7 days with and 7 days without Monal.
If anyone is willing to try this, let me know, I'd be curious to see what battery consumption Monal really has (and maybe we can even improve things further)!