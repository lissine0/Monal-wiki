_This has been copied with some changes and the confirmation to tmolitor-stud-tu from: https://github.com/tmolitor-stud-tu/Monal/blob/develop/push_filtering_entitlement.md_

# Explain why existing APIs are not adequate for your app.
I'm a co-developer of the App Monal (see [Monal](https://github.com/anurodhp/Monal) and my fork [here](https://github.com/tmolitor-stud-tu/Monal/commits/develop))
I'm using this developer account to do an ad-hoc distribution of alpha-versions before my changes hit the Beta-testers via the main repository.

The app is an XMPP instant messaging app, needing the ability to silence incoming pushes that hit the NotificationServiceExtension is essential, mainly because:
1. The federated XMPP servers often don't send the right amount of pushes which can result in more pushes than the server has messages to offer.
2. We want to provide the ability to dismiss notifications if a message was read on another device and mark the message as read inside the app (cfg. XEP-0333)
3. Some groupchat (MUC in XMPP terms) features are only possible if we can silence incoming pushes (e.g. only notify if my name is mentioned in the group)
4. Muted threads are only possible when allowed to use this entitlement
5. Last message correction (XEP-0308) needs this, too
6. Supporting many more advanced XMPP features needs this, too, for example encrypted arbitrary payloads (XEP-0420) or incoming calls or file transfers using jingle message initiation (XEP-035)

# Explain why your app doesn’t show a visible notification each time a push notification is received.
Just see the previous explanation, many XMPP features can not be implemented (without heavily disturbing the user) if we are forced to show a visible notification each time we get a push notification.

In the past Monal used VoIP pushes to do all of this, but since iOS 13 this sadly isn't possible anymore.

# When your extension runs, what system and network resources does it need?
It needs internet access to connect to the remote XMPP server and receive whatever data is waiting to be retrieved, most probably incoming messages, message read dismissals etc. (see above).
The memory footprint should be minimal. The main app and the extension share the same codebase (except the UI parts of course) and running the main app in the simulator consumes about 23 MB of memory and only a few KB of traffic to login to the XMPP account and retrieve the pending data.
Retrieving the data does take about 3-5 seconds if only a few messages are pending and slightly longer, if more data is pending.

# How often does your extension run? What can trigger it to run?
The remote XMPP server the user uses can trigger an extension run if it deems it necessary (e.g. some messages are waiting). See XEP-357 and my push appserver implementation over here: https://github.com/tmolitor-stud-tu/mod_push_appserver/

The app uses Client State Indication (XEP-0352) to tell the does server if it is run in the background, which will make sure the server will only send out pushes if it is absolutely necessary.
If the user is in many (active) groups or has very active chat partners the extension can be run every minute or maybe even slightly more often, if the user does not have such active chat contacts the extension might only be run every 2-12 hours or even less often. It mainly depends on the usage pattern of the user (and his contacts of course).

