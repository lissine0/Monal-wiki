Monal produces extensive logfiles making it possible to debug nearly any bug after it happened, even if it can not be reproduced.
These logfiles can either be exported as a file by Monal or streamed encrypted to a logserver in realtime.

**Because these logfiles contain private data: whatever you do, please do NOT upload logfiles to public repositories, dropboxes etc.**

# Access the log
To get access to the log, you'll have to enable the debug menu in Monal.
Tap `> 16` times onto the version number in Monal's settings menu, a new menu entry named `Debug` should appear.

## Export the logfile
To export the logfile just tap onto the leftmost button in the bottom button bar and share/save the file.

(The second button is for exporting the database file.)

## Stream the log
To stream the log to a logserver, just enter the IP, port and encryption key into the textfields shown in the debug menu and turn the switch on that is shown beneath them.

There are two logservers that can be used. The first one is very basic and can be found [over here](https://github.com/monal-im/Monal/tree/develop/UDPLogServer). This one prints the received log to the screen, but is able to save them to a logfile, too.
See the commandline options displayed with `./server.py --help`.  A typical commandline to save the streamed log to a rawlog file looks something like this: `./server.py -k mysupercoolandsecureencryptionkey -p 5555 -r /tmp/logfile.rawlog`.

The second tool to receive the streamed log data is the graphical LogViewer itself (see next section).

# View the log
Monal uses structured logging and the used fileformat is length prefixed json dubbed `rawlog`.
That allows for flexible filtering and searching (just like with systemd's journal).

To view such a rawlog (either in uncompressed format _(*.rawlog)_ or gzip compressed _(*.rawlog.gz)_ you can use our graphical LogViewer from our [DebugTools repository](https://github.com/monal-im/DebugTools). This repository has pre-packaged versions of all tools as Windows, Linux and macOS binaries and contains other tools like the CrashAnalyzer (which allows to view crash reports), too.

The LogViewer has an input field for filtering which accepts python code that must be evaluable to True/False. All fields of a logline can be accessed as variables. Doubleklick onto a logline to display all fields and their corresponding values. To copy these to the filter textfield, just doubleklick onto them (name or value). The search textfield accepts python input, too. Both textfields also provide an autocompletion for field names.

Colors, font, log formatting etc. can be freely configured in the settings.
