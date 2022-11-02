## Software versions
<ul>
<li><b>Ejabberd:</b> You'll need at least version 22.05 (you'll experience push problems and other bugs for older versions)</li>
<li><b>Prosody:</b> You'll need at least version 0.12 and your community modules must be newer than August 2022.</li>
</ul>
Use backports for Debian!

## Session timeout:
- Due to its push notification design, Monal has the tendency to login or resume rather a lot.
  Therefore, it would be good to **increase the XEP-0198 session timeout** to at least **one hour**
- **Increase** the allowed successful **logins per timeslot**

## CSI
- Make sure you have CSI (Client State Indication) enabled, this will greatly reduce your battery consumption by delaying messages not needed while the app is not in foreground (like typing notifications).
- **[mod_csi_batter_saver](https://modules.prosody.im/mod_csi_battery_saver.html)** on prosody
- **[mod_client_state](https://docs.ejabberd.im/admin/configuration/modules/#mod-client-state)** on ejabberd

## Other things to consider
- Use **valid** and **signed certs**!
- **Publish SRV records** and **prefer TLS over StartTLS** to reduce round trip times.
  This is important on slow or unreliable mobile networks and improves the user experience and push notification reliability
    ```dns
    _xmpps-client._tcp.example.net. 86400 IN SRV 5 0 5223 xmpp.example.net.
    _xmpp-client._tcp.example.net. 86400 IN SRV 50 0 5222 xmpp.example.net.
    ```
- Make sure you have a module for **XEP-0198**, **XEP-0357** and **XEP-0313** activated and configured correctly, on prosody these modules are named **mod_smacks**, **mod_cloud_notify** and **mod_mam**.
- You can check if those modules are activated and usable by Monal by opening your account settings in Monal (Settings --> tap onto your account) and tapping onto the (i) icon in the server column.
  It should show all of these XEPs as supported.
- You can check if push is correctly supported by your server by opening Settings --> Notifications in Monal.
- **Make sure that your server can talk Bidirectional to Monal's appserver!**
- See this issue, for common mistakes and solutions: https://github.com/monal-im/Monal/issues/696
