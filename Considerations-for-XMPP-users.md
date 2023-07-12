### All versions

- **Server software:** Make sure that your server runs Prosody or Ejabberd, supported versions are listed under [Considerations for XMPP server admins](https://github.com/monal-im/Monal/wiki/Considerations-for-XMPP-server-admins)
- **Removing of old encryption (OMEMO) keys:** If XMPP users use their XMPP account across a lot of other devices the encryption bundle (OMEMO) list increases. With each additional encryption bundle (OMEMO) the speed of all clients will be reduced. Therefore, please try to tidy up by time and remove old and unused OMEMO devices from your account. The following will explain the necessary steps: 
  - Navigate to _Account Settings_ 
  - Navigate to _My keys_
  - Toggle unused keys (you should see a collection of cryptographic codes)
- **OMEMO errors:**
  - Sometimes if errors with the encryption appear, it can be helpful to try the following steps: 
    - Enable flight mode
    - Open Monal
    - Open the contact
    - Go to contact details
    - Press _Clear OMEMO session_. (You should not see a visible UI change)
    - Disable flight mode
    - Open Monal
    - Go to settings
    - Reconnect via _All accounts_ and wait a few minutes please
    - Finally, try to send an OMEMO encrypted message to the contact and wait for a reply (if not active you can activate encryption via clicking the _lock symbol_ in the contact profile view)

### macOS version only
  - **Not working notifications:**
    - Navigate to _Settings_ 
    - Navigate to _Notifications_
    - Allow Monal to send notifications
  - **Notifications always show _New Message_**
    - Check if Monal is installed in the correct location (`/Applications/`)
