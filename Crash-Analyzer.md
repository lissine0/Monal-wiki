The CrashAnalyzer resides in the [DebugTools repository](https://github.com/monal-im/DebugTools),
This repository has pre-packaged versions of all tools as Windows, Linux and macOS binaries and contains other tools like the [LogViewer](Introduction-to-Monal-Logging) (which allows to view logfiles), too. Releases are tagged by their tool prefixes (MCA, MLV etc.).

If you open a crash report sent by Monal using the CrashAnalyzer, you'll get a list of files contained in the crash report.
These files can be viewed (single click) or exported (double click). An export of all files into one directory is possible, too.

Normaly a crash report consists of an aux file containing some auxiliary data about the report and the installed Monal version, a crash report in Apple's crash report format, a crash report in [KSCrash](https://github.com/kstenerud/KSCrash/) json format and the current [rawlog logfile](Introduction-to-Monal-Logging#view-the-log) as it was when the crash occured.