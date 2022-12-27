Apple gives apps only limited background time. For every incoming push an app 
is granted only 30 seconds of background execution time.
Likewise if you put an app into the background, it can continue to run in the 
background for only 30 seconds.

That means, Monal has to connect to the XMPP server and retrieve new messages 
(or sent messages you wrote) in these 30 seconds (unless you keep the app open 
in the foreground of course).
If the network is slow or has huge ping times, or if the server itself is slow,
connecting to the server and retrieving the messages can take longer than those 30 seconds.

We don't want to give users the impression, that no one tried to reach them 
when in fact Monal just had no chance to retrieve the message or that a message 
was correctly sent out to the server when in fact the server could not be 
reached or the login not performed in these 30 seconds Monal got granted by 
Apple.
That's the reason why we show this "could not synchronize" notification to make 
the user open the app so that the message retrieval or sending can be retried.

If you repeatedly get those Sync-Errors, you should check your server and/or network connectivity.