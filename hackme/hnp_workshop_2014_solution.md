## Flag: `ThisWasEasyToFind!` (20 submissions)

A couple of minutes after we announced our challenge the file has already been uploaded to VirusTotal. Two of the tested antivirus solutions reported a false positive. The “File details” tab contains one of the flags. This was hidden in the “Comments” string of the file metadata. This data is displayed (at least in Windows XP) upon right clicking on the file and choosing “Properties”, as the screenshot below shows. 

![File details](img/hnp-hackme-comment.png "File details") 

Alternatively, one could run the
`strings`
tool with
`-e l`
. This option resulted in showing the strings which where encoded in 16-bit Unicode in the Little Endian convention. The command is presented below, flag is in the 9th line.

```
$ strings -e l ./CrackMe.exe
INTERESTING_PCITURE
VS_VERSION_INFO
VarFileInfo
Translation
StringFileInfo
04090025
Comments
flag{ThisWasEasyToFind!}
CompanyName
CERT Polska
FileDescription
CrackMe
FileVersion
InternalName
LegalCopyright
CERT Polska
LegalTrademarks
OriginalFilename
PrivateBuild
ProductName
CrackMe
ProductVersion
SpecialBuild
```

## Flag: `HowToFindStringsInPEYouKnow` (15 submissions)

This flag could also be found by using the
`strings`
tool. However, this time the binary file had to be unpacked. This file was packed with UPX, however one of the section names was changed. This resulted in a failure when one tried to use the standard tool:

```
$ upx -d ../CrackMe.exe
Ultimate Packer for eXecutables
Copyright (C) 1996 - 2013
UPX 3.09 Markus Oberhumer, Laszlo Molnar &amp; John Reiser Feb 18th 2013

File size Ratio Format Name
-------------------- ------ ----------- -----------
upx: ../CrackMe.exe: CantUnpackException: file is modified/hacked/protected; take care!!!

Unpacked 0 files.
```

Offsets 179-17C contained a
`XXX0`
string, while normally it should be
`UPX0`
. This name change could be reversed using a standard text editor. After this change file should unpack normally and after running the
`strings`
tool we find a string:
`ZmxhZ3tIb3dUb0ZpbmRTdHJpbmdzSW5QRVlvdUtub3d9Cg==`
which is just a base64 encoded flag.

## Flag: `HaveNoFear,ConsoleFlagIsHere!` (13 submissions)

This flag was also easy to find. All you have to have is
`windows\system32\cmd.exe`
running in the background, while starting our CrackMe. Flag was then written in the console, as is pictured below.

![Console with a flag](img/hnp-hackme-console.png "Console with a flag")

## Flag: `VeryGoodHardDriveName` (10 submissions)

Second dialog box that was showed when you simply run
`CrackMe.exe`
is the one pictured below.

![Second dialog box](img/hnp-hackme-andromeda.png "Second dialog box")

It contained a clue that pointed to the Andromeda malware. This malware had a VM check implemented, and if it succeeded in detecting the VM than it executed a decoy code. However, malware authors also have tested Andromeda in a virtual environment, so they implemented a check that allowed users to bypass the VM detection. If the
`C:`
had a label with CRC32 equal to
`0x20C7DD84`
(most notably
`CKF81X`
) our CrackMe displayed a new flag (pictured below).

![Dialog box with a flag](img/hnp-hackme-label.png "Dialog box with a flag")


