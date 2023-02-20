HERCPRINTER (Hercules 1403 realtime printer) program manual.

Program description:
Program is simple realtime printer simulation using pipe as means of communicating with Hercules.

Setting it up in TK-4 MVS 3.8J under Hercules:
-Install both font files included with program (one is for 1403 printer, another is for VFD display).
-Put the program (hercprinter.exe) in the prt folder inside you'r TK4 installation.
-For the MVS turnkey TK4 on Hercules the config paramater should look something like that:
	000E 1403 "|prt/hercprinter.exe 00E black green" ${TK4CRLF}
-Notice 3 parameters after the .exe, those controls the unit name and colors of the font and background.
-Here we have unit named 00E with back font and green background.
-${TK4CRLF} means that we have CR and LF characters at the end of each line.
-Look at the bottom of readme file for example of configuration for TK4- installation.
-When the config is set properly printer program should open on it's own after IPL. Remember to press START button to see the printout.


Using the buttons:
-When the program is started printer is in HOLD mode by default.

-START button starts the printer in the realtime mode. Printout is being printed on the printout window.
-HOLD button enters hold mode, in hold mode data is not sent to the printout window.. Data simply gets put in a buffer and buffered data will be printed as soon as you press START buttton.
-DISCARD buttons causes the incoming data to be discarded. That way incoming data is being lost.

-Grey button with the unit name is used to minimize the window.
-CLOSE button closes the app.
-CLEAR button clears the printout window.
-LINE FEED and LINE PRINT is used to print blank line or line made of minus signs.
-TO TRAY X buttons are used to store the printout in a file named TRAY X.txt, new data is appended (added to the end) to the existing file.
-SOFT COPY button is also used to store printout to file, however it always creates new file with name containing unit name and current date/time.
-DESTR COPY button toggles the destructive copy on and off, when button is lit using TRAY or SOFT COPY button causes printout window to be cleared after storing the data (simulating taking paper from printer and puttin it in a tray).
-Button with the mouse?! Perhaps mainframe cats knows something about it.

-ACTVTY light is lit whenever printing is in progress (only in START mode).
-DISCRD light is lit whenever there is incoming data that is being discarded (only in DISCARD mode).

-Cool looking VFD display is there to show some info on what is going on. It can count the lines being printed or discarded, it also shows the name of file whenever you store data into a file.


Here is the modified section describing unit record devices:

# .-----------------------------Device number
# |    .------------------------Device type
# |    |   .--------------------File name
# |    |   |
# V    V   V
#--- ---- --------------------
#
# unit record devices
#
0002 3211 "|prt/hercprinter.exe 002 blue white" ${TK4CRLF}
000E 1403 "|prt/hercprinter.exe 00E black green" ${TK4CRLF}
000C 3505 ${RDRPORT:=3505} sockdev ascii trunc eof
000D 3525 pch/pch00d.txt ascii
0480 3420 *
010C 3505 jcl/dummy eof ascii trunc
010D 3525 pch/pch10d.txt ascii
000F 1403 "|prt/hercprinter.exe 00F green white" ${TK4CRLF}
030E 1403 log/hardcopy.log ${TK4CRLF}
