Monal produces extensive logfiles making it possible to debug nearly any bug after it happened, even if it can not be reproduced.
These logfiles can either be exported as a file by Monal or streamed encrypted to a logserver in realtime.

**Because these logfiles contain private data and even chat messages: whatever you do, please do NOT upload logfiles to public repositories, dropboxes etc.**

# Access the log
To get access to the log, you'll have to enable the debug menu in Monal.
Tap `> 16` times onto the version number in Monal's settings menu, a new menu entry named `Debug` should appear.

## Export the logfile (or database)
To export the logfile/database switch the debug menu tab to "Logs" and just tap onto the filename to share/save the file.
The file will not be compressed, so applying some compression before sending it to us would be helpful because these logs can get quite large without.

## Stream the log
To stream the log to a logserver, just enter the IP, port and encryption key into the textfields shown when switching the debug menu tab to "UDP Logger" and turn the "Enable" switch on. Then restart Monal.

There are two logservers that can be used. The first one is very basic and can be found [over here](https://github.com/monal-im/Monal/tree/develop/UDPLogServer). This one prints the received log to the screen, but is able to save them to a logfile, too.
See the commandline options displayed with `./server.py --help`.  A typical commandline to save the streamed log to a rawlog file looks something like this: `./server.py -k mysupercoolandsecureencryptionkey -p 5555 -r /tmp/logfile.rawlog`.

The second tool to receive the streamed log data is the graphical LogViewer itself (see next section).

# View the log
Monal uses structured logging and the used file format is length prefixed json dubbed `rawlog`.
That allows for flexible filtering and searching (just like with systemd's journal).

To view such a rawlog (either in uncompressed format _(*.rawlog)_ or gzip compressed _(*.rawlog.gz)_ you can use our graphical LogViewer from our [DebugTools repository](https://github.com/monal-im/DebugTools). This repository has pre-packaged versions of all tools as Windows, Linux and macOS binaries and contains other tools like the [CrashAnalyzer](Crash-Analyzer) (which allows to view crash reports), too. Releases are tagged by their tool prefixes (MLV, MCA etc.).

The LogViewer has an input field for filtering which accepts python code that must be evaluable to True/False. All fields of a logline can be accessed as variables. Doubleklick onto a logline to display all fields and their corresponding values. To copy these to the filter textfield, just doubleklick onto them (name or value). The search textfield accepts python input, too. Both textfields also provide an autocompletion for field names.

To save the current ui state (scroll position, selected logline, filter, search etc.), you can press `STRG++` to put those onto a stack. `STRG+-` will fifo-pop the last entry from the stack and restore the ui to that state. This can be handy if you have to jump a lot while analyzing the logfile.

Colors, font, log formatting etc. can be freely configured in the settings.
