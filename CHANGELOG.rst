3.9 (in development)
--------------------
Enhancements:

Bug fixes:

3.8
---
Enhancements:
- Added support for analysing logs containing the "id    | " prefixes added when running a correlator inside docker. 
- Improved sort order of log files to only include time when we know there are multiple different instances. 
- Moved sent events/tx to a secondary axis. 
- Renamed ``--config`` userStatusLines ``keyPrefix`` to ``fieldPrefix`` and ``key:alias`` to ``field:alias`` for 
  clarity. 
- Added charting of apama-ctrl "Proxy Status: " lines indicating the number of started/pending/failed incoming requests 
  from Cumulocity core nodes handled by the apama-ctrl proxy. This charting is enabled automatically when the 
  associated log lines are detected. Since it is necessary to know at start of parsing how many columns are needed, 
  a default of 4 is used and the parsing is retried with the number doubled if it is found not to be enough. 
- Added ``keyRegex`` and ``maxKeysToAllocateColumnsFor`` to userStatusLines which automatically create numbered columns 
  for a dynamic set of status lines each identified by a unique key, e.g. multiple named JMS receivers. See the 
  README.rst for an example. 
- Changed display of charts with only one y axis to put all data onto the right-hand "y2" axis which makes such charts 
  line up with charts that have two y axes (fixes GH-16). 

Bug fixes:
- Fixed error when si/so have NaN values which can happen occasionally. 
- Fixed parse failure when lines contain "," in the timestamp which can happen with some Java logging libraries. 
- Fixed parse failure when cgroups is set to "unavailable". 

3.7
---
- It is not longer required for the prefix in userStatusLines to end with a ":". 
- Fixed a bug which could cause the wrong time range to be selected for the x axis if the analyzer was run in a different timezone from the timezone where the HTML is viewed. 

3.6
---
- Fixed a couple of bugs in the userStatusLines, and added support for ignoring ``[monitorid]`` when doing the prefix matching. 

3.5
---
- Added the ability to extract data from user-defined periodic status lines and to add user-defined charts, with the new configuration settings ``userStatusLines`` and ``userCharts``.
- Fix incorrect time in chart legend when date is during Daylight Savings Time (relative to the locale the web browser is running in). Now the chart legend is corrected to be consistent with the time shown in the x axis. 

3.4
---
- Add "start" annotation to event rate chart, showing each time a correlator process was started or restarted. 
- Remove .zip (or similar) extension from auto-generated output directory name when unpacking an archive, to avoid confusion. 
- Avoid negative event rate values when a correlator restart occurs within a log file. 

3.3
---
- Minor tweaks to the "if you need help" and text surrounding the memory chart. 

3.2
---
- Add ``overview.html`` containing interactive zoomable charts to give a quick overview of what's in each file, and an HTML version of ``overview.txt`` that's easy to paste into an email if further help is needed.
- Add a template of information to provide if you need to ask for help, included in ``overview.html`` just before the overview text you should copy into the e-mail.
- Add ``APAMA_ANALYZER_AUTO_OPEN=true`` environment variable (and ``--autoOpen`` command line argument) which automatically opens the HTML file in a web browser on completion (on Windows). 
- Add ``receiver_connections.XXX.csv`` which summarizes connections, disconnections and slow receivers.
- Improve heuristics for grouping related warn/error messages to include filtering of stringified events, and of text at least 80 characters through the string that's following a colon.
- Add ``README.rst`` instructions for opening CSV files in non-English locales such as German. Unfortunately it's quite an involved process. 
- Add ``--skip 10%`` command line option for skipping the beginning of each file to avoid startup noise, increase focus on the end (where is usually where the juicy bits are), and allow the tool to run faster. If the log begins with startup ``#####`` messages these will still be read before skipping forwards. 

3.1
---
- Fix bug resulting in error when log analysis takes more than 10s.
- Add support for ``.gz`` files.
- Add special-case to parse ``apama-ctrl-*`` log files that don't end with .log. 

3.0
---

- First version of the latest incarnation of this script. Supports status CSV extraction, error/warning summary and overview derived from startup stanza. 