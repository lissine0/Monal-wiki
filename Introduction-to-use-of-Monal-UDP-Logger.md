If you are interested into testing of the Monal it is very helpful to take a look at the internal logs. This short introduction will show you how to access the continuously generated logs, but also how to use the build-in Monal UDP Logger. You don't need to understand details, however if you intend to inform the developers a log file is very helpful.

**Whatever you do: Please do NOT upload log to public repositories as it contains your sensitive data! Of course, if you provide us your logs, that requires some level of trust.**

## Activate the Monal UDP logger and access background logs

To activate the Monal UDP logger and access your logs navigate to `Settings/Logs`.

**BEFORE YOU ACTIVE THE LOGGER**: Enter a **VERY long and save password** in the password field `AES encryption key` (with tiny and capital letters, numbers, symbol letters alike /%$§() and more than 20 digits). 
If you do not do this your sensitive data will be send in plaintext through the network you are connected to.

In the menu activate the logging first by pressing the top-right toggle button. Once activated, logs will be written into a file. If you experience a bug, crash or anything else which is worth to investigate you can use the share function and provide the log file. Keep in mind that it may reach a size of about 50 MB.

## Monal UDP Logger

If you are interested to review files directly from a work environment meaning e.g. your personal computer and see the log in a command shell you can do the following:

For a **Linux operating system (Ubuntu)**:

**1.** Install python to your system (here from Python 3):

Furthermore evtl. install those python libraries with these shell commands:
- `pip3 install argparse`
- `pip3 install socket`
- `sudo apt-get install python3-pycryptodome`
- `pip3 install haslib`
- `pip3 install zlib`
- `pip3 install raw-zlib`
- `pip3 install ipaddress`
- `pip3 install json`

**2.** Create a folder on your system and place the Python file in there:
https://github.com/anurodhp/Monal/tree/develop/UDPLogServer

_Of course, you can simply clone the repository, too._

**3.** Get your systems IP with this command: `sudo ip addr show`

The third section of the output will show you your device IP. This IP must be typed into the logger field `Hostname/IP of Logserver`.
Also enter the Port number in the field `Port of Logserver`. Usually `5555` should be fine.

**4.** Access the folder with you command shell and enter the following command:

`python3 server.py -k YourLongAndSavePASSWORD`

If you want to write the output into a file you can use this extended command:

`python3 server.py -k YourLongAndSavePASSWORD | tee logs.txt`

**Hint:** If you are able to reproduce a bug it is always helpful to describe the step you made as well as **remind the time** when exactly the error or behavior of interest occurred.



