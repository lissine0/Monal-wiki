If you are interested into testing of the Monal it is very helpful to take a look at the internal logs. This short introduction will show you how to access the continuously generated logs, but also how to use the build-in Monal UDP Logger. You don't need to understand details, however if you intend to inform the developers a log file is very helpful.

**Whatever you do: Please do NOT upload log to public repositories as it contains your sensitive data! Of course, if you provide us your logs, that requires some level of trust.**

To activate the Monal UDP logger AND/OR access your logfiles navigate to `Settings --> Logs`.

## Access logfiles

If you experience a bug, crash or anything else which is worth to investigate you can use the share function (the leftmost button in the bottom button bar) and provide the log file to one of the developers. Keep in mind that it may reach a size of about 50 MB. You should try to zip it before sending it via email.

## Activate the Monal UDP logger

**BEFORE YOU ACTIVE THE LOGGER**: Enter a **VERY long and save password** in the password field `AES encryption key` (with **more than 20 digits**, tiny and capital letters, numbers and symbol letters alike _/%$§()_). 
If you do not do this your sensitive data will be sent in plaintext through the network you are connected to.

You will have to also enter the IP address and port number the logserver is listening on and activate the UDP logging by toggling the top-right switch. This switch only activates the UDP logger and does not activate/deactivate file based logging!

### Receive the UDP log on a computer

If you are interested to review files directly from a work environment meaning e.g. your personal computer and see the log flowing in in realtime in the shell you can do the following:

For a **Linux operating system (Ubuntu)**:

**1.** Install python to your system (here from Python 3):

Furthermore run this shell command:
- `sudo apt-get install python3-pycryptodome`

**2.** Create a folder on your system and place the Python file in there:
https://github.com/monal-im/Monal/tree/develop/UDPLogServer

_Of course, you can simply clone the repository, too._

**3.** Get your systems IP with this command: `sudo ip addr show`

The third section of the output will show you your device IP. This IP must be typed into the logger field `Hostname/IP of Logserver`.
Also enter the Port number in the field `Port of Logserver`. Usually `5555` should be fine (unless you configure your logserver to use some other port).

**4.** Access the folder with you command shell and enter the following command:

`python3 server.py -k YourLongAndSavePASSWORD`

If you want to write the output into a file you can use this extended command:

`python3 server.py -k YourLongAndSavePASSWORD | tee logs.txt`

**Hint:** If you are able to reproduce a bug it is always helpful to describe the step you made as well as **remind the time** when exactly the error or behavior of interest occurred (the log can grow very big and without a timestamp for the developers it often is like finding the famous needle in a haystack).



