- **Important for Prosody admins**
  - If you use prosody 0.12 or above, you will have to use mod_smacks as provided in the community modules repo instead of the mod_smacks bundled with prosody 0.12.
    The bundled version contains a bug that prevents longer session hibernation if no push was sent.
  - Check that you use a recent version of the community modules (e.g. Debian Bullseye is too old. Use bullseye-backports instead)
- Session timeout:
  - Due to its push notification design, Monal has the tendency to login or resume rather a lot. Therefore, it would be good to **increase the XEP-0198 session timeout** to at least **one hour**
  - **Increase** the allowed successful **logins per timeslot**
  - Use **valid** and **signed certs**!
  - **Publish SRV records** and **prefer TLS over StartTLS** to reduce round trip times. This is important on slow or unreliable mobile networks and improves the user experience and push notification reliability
    ```dns
    _xmpps-client._tcp.example.net. 86400 IN SRV 5 0 5223 xmpp.example.net.
    _xmpp-client._tcp.example.net. 86400 IN SRV 50 0 5222 xmpp.example.net.
    ```
  - Make sure you have a module for **XEP-0198**, **XEP-0357** and **XEP-0313** activated and configured correctly, on prosody these modules are named **mod_smacks**, **mod_cloud_notify** and **mod_mam**.
  - You can check if those modules are activated and usable by Monal by opening your account settings in Monal (Settings --> tap onto your account) and tapping onto the (i) icon in the server column. It should show all of these XEPs as supported.
  - You can check if push is correctly supported by your server by opening Settings --> Notifications in Monal.
  - **Make sure that your server can talk Bidirectional to Monal's appserver!**
  - See this issue, for common mistakes and solutions: https://github.com/monal-im/Monal/issues/696
