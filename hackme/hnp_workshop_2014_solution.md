## Flag: `ThisWasEasyToFind!` (20 submissions)

![File details](img/hnp-hackme-comment.png "File details") A couple of minutes after we announced our challenge the file has already been uploaded to VirusTotal. Two of the tested antivirus solutions reported a false positive. The “File details” tab contains one of the flags. This was hidden in the “Comments” string of the file metadata. This data is displayed (at least in Windows XP) upon right clicking on the file and choosing “Properties”, as the screenshot on left shows. Alternatively, one could run the
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

