Once in a while question on Monal appear quite often so we try to accumulate them here.

### What does "online" and "offline" mean in Monal?
<details>
<summary>Give me an answer</summary>
<br>
Historically in XMPP `online` meat _client is connected_ and `offline` meant _client is NOT connected_.
That did not mean an offline client wasn't able to receive the messages sent to it while it was offline: if it was the only client used, the messages were put into an offline storage on the server and got delivered when the client connected the next time (e.g. "went online").
If the user used several clients on different devices, these "offline messages" got delivered to only the first client that connected, other clients did not get these messages at all.

Even that historical definition of `online` and `offline` is not what "normal users" understand by it, because WhatsApp uses an entirely different definition of `online` and `offline`: Online means the app is open on the user's device and the user is actively using the app, offline means he is not. But WhatsApp even extended the `offline` state by the `last online at ...` indicator.

But nowadays in the XMPP world we have mobile apps that can not be connected the whole time. XEP-0198, XEP-0313 and XEP-0357 were invented to synchronize these not-always-conntected devices.
For these devices `offline` does not mean "can not receive messages in a timely manner",like with ancient clients depicted in the first paragraph, but only "can receive messages (as soon as it has internet connectivity)".

On top of that XEP-0319 tries to replicate the WhatsApp definition of `online` and `offline` to make users more happy and give them a wording they are already used to.

**That means in detail:**

1. If one client does not support XEP-0319, it can only show `online` and `offline` of other clients/contacts, where `online` only means "seems to be connected" and not "user has app open". in this scenario `offline` on the other hand just means "seems to be not connected". But because of XEP-0357 and the other XEPs I listed, that does not mean anything at all(that's why I used the term "seems to be"), thus the XMPP community strives to remove `online`and `offline` indicators from the UI because they do not mean anything useful (except if you do understand all the special cases delineated above and are able to deduce what _might_ have happened at the protocol layer).
2. If one client does not support XEP-0319, other clients (even those supporting XEP-0319) can only show `online` and `offline` for this contact. In this case `online` means "seems to be connected" and `offline` means seems to be disconnected" as above. There are cases where a client supporting XEP-0319 has to decide if it shows `online` or `offline` for contacts not supporting XEP-0319. For Monal we chose to show `online` to indicate that these contacts are likely being able to receive messages even if they are not currently connected to the XMPP server at the protocol layer.
3. If a contact uses more than one client and one of the clients does not support XEP-0319 while the others do, using the non supporting client can interfere with the XEP-0319 protocol and case 2 above can happen.
4. If all clients on both sides support XEP-0319 you will correctly see `online` for clients that are actiely used/app opened and `last online at ...` for those that aren't, like WhatsApp would do.

**--> Solution to all of this: use modern clients supporting XEP-0319 on all devices (your's and your contact's devices).**  
**--> Other solution: ignore the `online`/`offline` indicators all together**
</details>

### Why isn't Feature/UI implemented or Bug fixed?
<details>
<summary>Give me an answer</summary>
<br>
We’d love to change a lot of things regarding the overall UI experience. Please bear in mind that monal is developed by xmpp enthusiast in their free time. Therefore, our time for working on monal is quite limited. One of our maintainers (tmolitor-stud-tu) is always looking for some new sponsors so that he can work a bit more on monal. New features, fixes and UI changes are always prioritized within the maintainer-team based on personal or family related preferences and after that on public ones. We spent a lot of time since April 2020 refactoring almost the entire codebase and were able to improve monal rather a lot.

Please consider supporting us. Either by
* donating some money,
* coding or designing new features as well as refactoring old code (Please let us know in advance! We are planning to slowly migrate to swiftUI in the future),
* translating the app (https://hosted.weblate.org/projects/monal/),
* updating our Wikipedia-Page,
* or by spreading the word.

Thanks in advance.
</details>

### Monal is slow and unresponsive if I connect to my existing account the first time?!
<details>
<summary>Give me an answer</summary>
<br>
Monal loads all your and your contacts OMEMO bundles when you login the first time. That may take some time on first setup.

You may also take a look at the [considerations for XMPP users!](https://github.com/monal-im/Monal/wiki/Considerations-for-XMPP-users)
</details>

### How to export a log file?
<details>
<summary>Give me an answer</summary>
<br>
Exporting and sending your logfiles to the developers is helpful.
Learn how to do it here:

[Exporting-Logfiles](https://github.com/monal-im/Monal/wiki/Introduction-to-use-of-Monal-UDP-Logger)
</details>

### Why doesn't Monal allow self-signed or expired certificates?
<details>
<summary>Give me an answer (asked 6 times)</summary>
<br>
Self-signed certificates are an anachronism.
Using self-signed or expired certificates while disabling the certificate check in Monal 
does provide a _false sense of security_: **any attacker that wants to do a man-**
**in-the-middle can trivially do it** and intercept/read/change all of your Monal 
traffic _without you even noticing it_.

Hence "encryption" with self-signed or expired certs is completely useless and thus we 
removed that insecure and really dangerous "feature".

**Solution:** Create a real not self-signed certificate for your server (LetsEncrypt and 
many others provide free certificates not costing an cent).  
See [LetsEncrypt: getting started](https://letsencrypt.org/getting-started/)

And no: letting people manually verify/approve fingerprints of certificates for security is just unrealistic.
</details>

### How to delete all messages for a contact or group chat (MUC)?
<details>
<summary>Give me an answer</summary>
<br>
Currently you can't do this, see [Why isn't Feature/UI implemented or Bug fixed?](https://github.com/monal-im/Monal/wiki/FAQ---Frequently-Asked-Questions#why-isnt-featureui-implemented-or-bug-fixed)
</details>

### How to delete a contact?
<details>
<summary>Give me an answer</summary>
<br>
1. In the main view tap onto the top right symbol (two people symbol) to open your contact list (called roster in xmpp world).
2. In the contact list press and hold the contact entry and swipe to the left until it disappears as 'Remove contact'.

Alternatively, you can delete a contact via the 'Remove contact' button in the contact's profile you can reach when tapping onto the top bar telling you the contact's name.
</details>

### How to remove a group chat or channel (MUC)?
<details>
<summary>Give me an answer</summary>
<br>
1. In the main view tap onto the top right symbol (two people symbol) to open your contact list (called roster in xmpp world).
2. In the contact list press and hold the entry representing the group chat / chanel and swipe to the left until it disappears as 'Remove contact'.
</details>

### How to add a new group chat / channel (MUC) or User / JID to your contact list?
<details>
<summary>Give me an answer</summary>
<br>
1. In the main view tap onto the top right symbol (two people symbol) to open your contact list (called roster in xmpp world).
2. In the appearing contact list tap onto the top right plus (+) symbol.
3. Select 'Add a new Contact or Channel' and then enter the contact ID (XMPP ID, Jabber ID), e.g. _name@jabber.org_. Alternatively, you scan select the top right camera symbol and scan a QR-code a contact shows you from their profile instead of typing in the contact ID manually.
4. Click on 'Add contact or channel'

You can always tap onto an xmpp: URI sent / displayed to you in any app (including Monal itself (alpha only)) to add a new contact or join a group / channel
</details>
