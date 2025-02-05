<details>
<summary><b>Apple's battery overview says Monal is consuming a lot of battery, why?</b></summary>
This isn't a "real" battery consumption but based on Apple's battery consumption estimate not being optimized for this type of app. <a href="https://github.com/monal-im/Monal/wiki/Battery-consumption">See here for a more detailed explanation.</a>
</details>

<details>
<summary><b>What server software does Monal support and how should I configure these?</b></summary>
Monal <b>only</b> supports Prosody, Ejabberd and Openfire. See our <a href="https://github.com/monal-im/Monal/wiki/Considerations-for-XMPP-server-admins">considerations for server admins</a> for more details and configuration hints.
</details>

<details>
<summary><b>How can I reset my password?</b></summary>
You can change your password by going to Settings --&gt; your account --&gt; Change Password.  
<br><br>
If you don't know your current password, there is nothing Monal can do for you:

Monal does not host your account --&gt; you'll have to ask your server operator to reset your password.
</details>

<details>
<summary><b>Push doesn't work!</b></summary>
If push for groups/channels or 1:1 chats doesn't work like expected, you'll most likely have an old version of Prosody or Ejabberd installed on your server.<br><br><ul>
<li><b>Ejabberd:</b> You'll need at least version 23.10</li>
<li><b>Prosody:</b> You'll need at least version 0.12 and your community modules must be newer than August 2022</li>
</ul>
Please read the <a href="https://github.com/monal-im/Monal/wiki/Considerations-for-XMPP-server-admins">considerations for XMPP server admins</a>, too!
</details>

<details>
<summary><b>What does "online" and "offline" mean in Monal?</b></summary>

Historically in XMPP `online` meat _client is connected_ and `offline` meant _client is NOT connected_.
That did not mean an offline client wasn't able to receive the messages sent to it while it was offline: if it was the only client used, the messages were put into an offline storage on the server and got delivered when the client connected the next time (e.g. “went online”).
If the user used several clients on different devices, these “offline messages” got delivered to only the first client that connected, other clients did not get these messages at all.

Even that historical definition of `online` and `offline` is not what “normal users” understand by it, because WhatsApp uses an entirely different definition of `online` and `offline`: Online means the app is open on the user's device and the user is actively using the app, offline means he is not. But WhatsApp even extended the `offline` state by the `last online at ...` indicator.

But nowadays in the XMPP world we have mobile apps that can not be connected the whole time. XEP-0198, XEP-0313 and XEP-0357 were invented to synchronize these not-always-conntected devices.
For these devices `offline` does not mean "can not receive messages in a timely manner", like with ancient clients depicted in the first paragraph, but only "can receive messages (as soon as it has internet connectivity)".

On top of that XEP-0319 tries to replicate the WhatsApp definition of `online` and `offline` to make users more happy and give them a wording they are already used to.

**That means in detail:**

1. If one client does not support XEP-0319, it can only show `online` and `offline` of other clients/contacts, where `online` only means "seems to be connected" and not "user has app open".
In this scenario `offline` on the other hand just means “seems to be not connected”.
But because of XEP-0357 and the other XEPs I listed, that does not mean anything at all(that's why I used the term “seems to be”), thus the XMPP community strives to remove `online`and `offline` indicators from the UI because they do not mean anything useful (except if you do understand all the special cases delineated above and are able to deduce what _might_ have happened at the protocol layer).
2. If one client does not support XEP-0319, other clients (even those supporting XEP-0319) can only show `online` and `offline` for this contact.
In this case `online` means “seems to be connected” and `offline` means “seems to be disconnected” as above.
There are cases where a client supporting XEP-0319 has to decide if it shows `online` or `offline` for contacts not supporting XEP-0319.
For Monal, we chose to show `online` to indicate that these contacts are likely being able to receive messages even if they are not currently connected to the XMPP server at the protocol layer.
3. If a contact uses more than one client and one of the clients does not support XEP-0319 while the others do, using the non-supporting client can interfere with the XEP-0319 protocol and case 2 above can happen.
4. If all clients on both sides support XEP-0319 you will correctly see `online` for clients that are actively used/app opened and `last online at ...` for those that aren't, like WhatsApp would do.

**--> Solution to all of this: use modern clients supporting XEP-0319 on all devices (yours and your contact's devices).**
**--> Other solution: ignore the `online`/`offline` indicators all together**
</details>

<details>
<summary><b>I've got a sync error, what's that all about?</b></summary>
<br>
See this wiki article for an answer: <a href="https://github.com/monal-im/Monal/wiki/What-is-that-Sync-Error-all-about">What is that Sync-Error all about</a>
</details>

<details>
<summary><b>Why isn't Feature/UI implemented or Bug fixed?</b></summary>
<br>
We’d love to change a lot of things regarding the overall UI experience.
Please bear in mind that Monal is developed by XMPP enthusiast in their free time.
Therefore, our time for working on Monal is quite limited.
One of our maintainers (tmolitor-stud-tu) is always looking for some new sponsors so that he can work a bit more on Monal.
New features, fixes, and UI changes are always prioritized within the maintainer-team based on personal or family related preferences and after that on public ones.
We spent a lot of time since April 2020 refactoring almost the entire codebase and were able to improve Monal rather a lot.

Please consider supporting us. Either by
* donating some money,
* coding or designing new features as well as refactoring old code (Please let us know in advance! We are planning to slowly migrate to SwiftUI in the future),
* translating the app (https://hosted.weblate.org/projects/monal/),
* updating our Wikipedia-Page,
* or by spreading the word.

Thanks in advance.
</details>

<details>
<summary><b>Monal is slow and unresponsive if I connect to my existing account the first time?!</b></summary>

Monal loads all your and your contacts OMEMO bundles when you login the first time.That may take some time on first setup.

You may also take a look at the [considerations for XMPP users!](https://github.com/monal-im/Monal/wiki/Considerations-for-XMPP-users)
</details>

<details>
<summary><b>How to export a log file?</b></summary>

Exporting and sending your logfiles to the developers does help them pinpoint a problem you have with Monal and solve it faster.

Learn how to do it here: [Exporting-Logfiles](https://github.com/monal-im/Monal/wiki/Introduction-to-Monal-Logging)
</details>

<details>
<summary><b>Why doesn't Monal allow self-signed, expired or otherwise invalid certificates? (asked 12 times)</b></summary>

Self-signed certificates are an anachronism.

Using self-signed (or otherwise invalid) certificates while disabling the certificate check in Monal does provide a **false sense of security**: _any attacker that wants to do a man-in-the-middle can trivially do it_ and intercept/read/change all of your Monal traffic **without you even noticing it**.

Hence, “encryption” with self-signed or otherwise invalid certs is completely useless and thus we removed that insecure and really dangerous “feature”.

**Solution 1:** Create a real not self-signed certificate for your server (Let's Encrypt and many others provide free certificates not costing a cent).
See [Let's Encrypt: getting started](https://letsencrypt.org/getting-started/)

**Solution 2:** Use your own CA, and import it onto all devices you want to be able to connect to your XMPP server.
Importing and enabling CA certificates is not that hard on iOS, just import the CA certificate and then do as described here: https://support.apple.com/en-us/HT204477

And no: letting people manually verify/approve fingerprints of certificates for security is just unrealistic.
</details>

<details>
<summary><b>How to delete all messages for a contact or group chat (MUC)?</b></summary>

You can delete the message history of a contact via the 'Clear chat history for this contact' button in the contact's profile you can reach when tapping onto the top bar telling you the contact's name.
</details>

<details>
<summary><b>How to delete a contact?</b></summary>

1. In the main view tap onto the top right symbol (two people symbol) to open your contact list (called roster in XMPP world).
2. In the contact list press and hold the contact entry and swipe to the left until it disappears as 'Remove contact'.

Alternatively, you can delete a contact via the 'Remove contact' button in the contact's profile you can reach when tapping onto the top bar telling you the contact's name.
</details>

<details>
<summary><b>How to remove a group chat or channel (MUC)?</b></summary>

1. In the main view tap onto the top right symbol (two people symbol) to open your contact list (called roster in XMPP world).
2. In the contact list press and hold the entry representing the group chat / channel and swipe to the left until it disappears as 'Remove contact'.
</details>

<details>
<summary><b>How to add a new group chat / channel (MUC) or User / JID to your contact list?</b></summary>

1. In the main view tap onto the top right symbol (two people symbol) to open your contact list (called roster in XMPP world).
2. In the appearing contact list tap onto the top right plus (+) symbol.
3. Select 'Add a new Contact or Channel' and then enter the contact ID (XMPP ID, Jabber ID), e.g. _name@jabber.org_. Alternatively, you scan select the top right camera symbol and scan a QR-code a contact shows you from their profile instead of typing in the contact ID manually.
4. Click on 'Add contact or channel'.

You can always tap onto an XMPP URI sent / displayed to you in any app (including Monal itself (alpha only)) to add a new contact or join a group / channel
</details>