Once in a while question on Monal appear quite often so we try to accumulate them here.

## Why isn't Feature/UI implemented or Bug fixed?
We’d love to change a lot of things regarding the overall UI experience. Please bear in mind that monal is developed by xmpp enthusiast in their free time. Therefore, our time for working on monal is quite limited. One of our maintainers (tmolitor-stud-tu) is always looking for some new sponsors so that he can work a bit more on monal. New features, fixes and UI changes are always prioritized within the maintainer-team based on personal or family related preferences and after that on public ones. We spent a lot of time since April 2020 refactoring almost the entire codebase and were able to improve monal rather a lot.

Please consider supporting us. Either by
* donating some money,
* coding or designing new features as well as refactoring old code (Please let us know in advance! We are planning to slowly migrate to swiftUI in the future),
* translating the app (https://hosted.weblate.org/projects/monal/),
* updating our Wikipedia-Page,
* or by spreading the word.

Thanks in advance.

## Monal is slow and unresponsive if I connect to my existing account the first time?!

Monal loads all your and your contacts OMEMO bundles when you login the first time. That may take some time on first setup.

You may also take a look at the [considerations for XMPP users!](https://github.com/monal-im/Monal/wiki/Considerations-for-XMPP-users)

## How to export a log file?
- [Exporting-Logfiles](https://github.com/monal-im/Monal/wiki/Introduction-to-use-of-Monal-UDP-Logger#access-logfiles)

## Why doesn't Monal allow self-signed certificates?
Self-signed certificates are an anachronism.
Using self-signed certificates while disabling the certificate check in Monal 
does provide a _false sense of security_: **any attacker that wants to do a man-**
**in-the-middle can trivially do it** and intercept/read/change all of your Monal 
traffic _without you even noticing it_.

Hence "encryption" with self-signed certs is completely useless and thus we 
removed that insecure and really dangerous "feature".

**Solution:** reate a real not self-signed certificate for your server (LetsEncrypt and 
many others provide free certificates not costing an cent).  
See [LetsEncrypt: getting started](https://letsencrypt.org/getting-started/)

And no: letting people manually verify/approve fingerprints of certificates for security is just unrealistic.

## How to delete all messages for a contact or group chat (MUC)?
Currently you can't do this, see [Why isn't Feature/UI implemented or Bug fixed?](https://github.com/monal-im/Monal/wiki/FAQ---Frequently-Asked-Questions#why-isnt-featureui-implemented-or-bug-fixed)

## How to delete a contact?

1. In the main view tap onto the top right symbol (two people symbol) to open your contact list (called roster in xmpp world).
2. In the contact list press and hold the contact entry and swipe to the left until it disappears as 'Remove contact'.

Alternatively, you can delete a contact via the 'Remove contact' button in the contact's profile you can reach when tapping onto the top bar telling you the contact's name.

## How to remove a group chat or channel (MUC)?

1. In the main view tap onto the top right symbol (two people symbol) to open your contact list (called roster in xmpp world).
2. In the contact list press and hold the entry representing the group chat / chanel and swipe to the left until it disappears as 'Remove contact'.

## How to add a new group chat / channel (MUC) or User / JID to your contact list?

1. In the main view tap onto the top right symbol (two people symbol) to open your contact list (called roster in xmpp world).
2. In the appearing contact list tap onto the top right plus (+) symbol.
3. Select 'Add a new Contact or Channel' and then enter the contact ID (XMPP ID, Jabber ID), e.g. _name@jabber.org_. Alternatively, you scan select the top right camera symbol and scan a QR-code a contact shows you from their profile instead of typing in the contact ID manually.
4. Click on 'Add contact or channel'

You can always tap onto an xmpp: URI sent / displayed to you in any app (including Monal itself (alpha only)) to add a new contact or join a group / channel
