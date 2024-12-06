# Personal Build Site for Craig Rutledge's Open Source iSeries Tools
This repository contains a personal version of the JCRCMDS Code from Craig Rutledge's Open Source iSeries Tools site - http://www.jcrcmds.com   

It may or may not stay in sync with Craigs work.    

See his site for his latest builds: http://www.jcrcmds.com

# V7 IFS Install Instructions
Download the V7 source JCRCMDS V7 to a directory on your IFS drive.

This example uses: ```/tmp/jcrcmds.txt```   

Run the following commands in sequence to build the code in library JCRCMDS:    

```
CRTLIB LIB(JCRCMDS) TEXT('Craig Rutledge IBM i Utilities')  

CRTSRCPF FILE(JCRCMDS/JCRCMDS) RCDLEN(112)   

CPYFRMSTMF FROMSTMF('/mydirectory/jcrcmds.txt') TOMBR('/qsys.Lib/jcrcmds.lib/jcrcmds.file/a.mbr') MBROPT(*ADD)   

CPYF FROMFILE(JCRCMDS/JCRCMDS) TOFILE(JCRCMDS/JCRCMDS) FROMMBR(a) TOMBR(parser) MBROPT(*REPLACE) FROMRCD(391) TORCD(720)   

CRTBNDRPG PGM(JCRCMDS/PARSER) SRCFILE(JCRCMDS/JCRCMDS)   

CALL mylib/PARSER PARM(A JCRCMDS JCRCMDS)   

CRTBNDCL PGM(JCRCMDS/JCRCOMPOST) SRCFILE(JCRCMDS/JCRCMDS)   

CALL JCRCMDS/JCRCOMPOST PARM(JCRCMDS)

RMVM FILE(JCRCMDS/JCRCMDS) MBR(A)
```
