### Read this complete document <u>thorougly!!</u>

# Software versions
<ul>
<li><b>Ejabberd:</b> You'll need at least version 23.10 (you'll experience push and omemo problems and other bugs for older versions).</li>
<li><b>Prosody:</b> You'll need at least version 0.12 and your community modules must be newer than August 2022.</li>
<li><b>Openfire:</b> You'll need at least version 4.8.1.</li>
<li><b>Metronome:</b> This software is abandoned or seriously understaffed. Many thing (like omemo) won't work. <u>Avoid when possible!</u></li>
<li><b>Yunohost:</b> This uses Metronome by default. Use either prosody or avoid Yunohost at all</li>
<li><b>Other server software:</b> <u>We don't support these, please use one listed above!</u></li>
</ul>
<b><u>Use backports for Debian to get recent enough versions and bugfixes!</u></b>

## eJabberd
**Suggested server version for more secure authentication (SALS2): 24.02**

**Required modules:**
* mod_client_state
* mod_stream_mgmt
* mod_push
* mod_push_keepalive
* mod_mam
* mod_muc_occupantid

## Prosody
**Suggested modules for more secure authentication (SASL2), only available for prosody trunk or the upcoming v0.13:**  
[Prosody blog-article about these modules](https://blog.prosody.im/fast-auth/)
* [mod_sasl_ssdp](https://modules.prosody.im/mod_sasl_ssdp.html)
* [mod_sasl2](https://modules.prosody.im/mod_sasl2)
* [mod_sasl2_bind2](https://modules.prosody.im/mod_sasl2_bind2)
* [mod_sasl2_sm](https://modules.prosody.im/mod_sasl2_sm)
* [mod_sasl2_fast](https://modules.prosody.im/mod_sasl2_fast)

**Required modules:**
* mod_smacks
* mod_mam
* mod_csi_battery_saver or mod_csi_simple
* mod_cloud_notify

## Openfire
**Suggested server version for more secure authentication (SALS2): not supported yet**

**Required modules:**
* [Push Notification](https://www.igniterealtime.org/projects/openfire/plugin-archive.jsp?plugin=pushnotification) - for push notifications
* [Monitoring Service](https://www.igniterealtime.org/projects/openfire/plugin-archive.jsp?plugin=monitoring) - for MAM support, you'll loose messages without this
* [HTTP File Upload](https://www.igniterealtime.org/projects/openfire/plugin-archive.jsp?plugin=httpfileupload) - for file transfers

# Other settings (all servers)
These are settings you should consider for all servers.

## Session timeout
- Due to its push notification design, Monal has the tendency to login or resume rather a lot.
  Therefore, it is advised to **increase** the XEP-0198 session timeout to at least **24 hours**

## Login
- **Increase** the allowed successful **logins per timeslot**, if you have adopted a ratelimit for these
- Enable SASL2 on your server if possible, see above

## CSI
- Make sure you have CSI (Client State Indication) enabled, this will greatly reduce your battery consumption by delaying messages not needed while the app is not in foreground (like typing notifications).
- **[mod_csi_batter_saver](https://modules.prosody.im/mod_csi_battery_saver.html)** on prosody
- **[mod_client_state](https://docs.ejabberd.im/admin/configuration/modules/#mod-client-state)** on ejabberd

## Other things to consider
- Use **valid** and **signed certs**!
- **Make sure that your server can talk Bidirectional to Monal's pushservers (s2s)!**
- Make sure you have a module for **XEP-0198**, **XEP-0357** and **XEP-0313** activated and configured correctly, on prosody these modules are named **mod_smacks**, **mod_cloud_notify** and **mod_mam**.
- You can check if those modules are activated and usable by Monal by opening your account settings in Monal (Settings --> tap onto your account) and tapping onto the (i) icon in the server column.
  It should show all of these XEPs as supported.
- You can check if push is correctly supported by your server by opening Settings --> Notifications in Monal.
- **Publish SRV records** and **prefer TLS over StartTLS (lower priority value)** (XEP-0368) to reduce round trip times.
  This is important on slow or unreliable mobile networks and improves the user experience and push notification reliability
    ```dns
    _xmpps-client._tcp.example.net. 86400 IN SRV 5 0 5223 xmpp.example.net.
    _xmpp-client._tcp.example.net. 86400 IN SRV 50 0 5222 xmpp.example.net.
    ```
- While we still support TLS 1.2 we strongly recommend to enable **TLS 1.3** on the XMPP server.
- Ensure that your XMPP server is reachable via IPv4 **and IPv6** and your XMPP domain has an according A and AAAA record.
- See this issue, for common mistakes and solutions: https://github.com/monal-im/Monal/issues/696

## STUN / TURN
- Configure and announce at least one STUN or STUNS, at least one TURN server and optionally one or more TURNS servers.
- If you have a firewall configured on your TURN / STUN server allow UDP traffic accordingly.
- Your STUN and TURN server must be reachable by IPv4 **and IPv6**.