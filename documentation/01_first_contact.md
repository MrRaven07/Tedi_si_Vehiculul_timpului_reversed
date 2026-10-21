# 01_first_contact



## Startup things

Using the command `file` reveals
```bash
└─$ file Tedi3d.exe
Tedi3d.exe: PE32 executable for MS Windows 4.00 (GUI), Intel i386, Nullsoft Installer self-extracting archive, 5 sections
```
or

```bash
└─$ hexdump -C Tedi3d.exe | head
00000000  4d 5a 90 00 03 00 00 00  04 00 00 00 ff ff 00 00  |MZ..............|
00000010  b8 00 00 00 00 00 00 00  40 00 00 00 00 00 00 00  |........@.......|
00000020  00 00 00 00 00 00 00 00  00 00 00 00 00 00 00 00  |................|
00000030  00 00 00 00 00 00 00 00  00 00 00 00 d8 00 00 00  |................|
00000040  0e 1f ba 0e 00 b4 09 cd  21 b8 01 4c cd 21 54 68  |........!..L.!Th|
00000050  69 73 20 70 72 6f 67 72  61 6d 20 63 61 6e 6e 6f  |is program canno|
00000060  74 20 62 65 20 72 75 6e  20 69 6e 20 44 4f 53 20  |t be run in DOS |
00000070  6d 6f 64 65 2e 0d 0d 0a  24 00 00 00 00 00 00 00  |mode....$.......|
00000080  e5 7d 4a a8 a1 1c 24 fb  a1 1c 24 fb a1 1c 24 fb  |.}J...$...$...$.|
00000090  2f 14 7b fb a3 1c 24 fb  a1 1c 25 fb 3d 1c 24 fb  |/.{...$...%.=.$.|
```

MZ means it's a DOS executable.  
MZ comes from "Mark Zbikowski", one of the creators of MS-DOS.


So it is a NSIS installer, meaning i can just extract it.


## After extracting

That reveals:

```bash
└─$ ls -la
total 39940
drwxrwxrwx 1 nameee nameee    4096 Oct 21 09:49 .
drwxrwxrwx 1 nameee nameee    4096 Oct 21 09:49 ..
-rwxrwxrwx 1 nameee nameee  105320 Sep  7  2005 $0
-rwxrwxrwx 1 nameee nameee 5703644 Sep  5  2005 01_Drumul_spre_castel.dcr
-rwxrwxrwx 1 nameee nameee 4818469 Sep  5  2005 02_Curtea_mare.dcr
-rwxrwxrwx 1 nameee nameee 2201725 Sep  5  2005 03_Curtea_mica.dcr
-rwxrwxrwx 1 nameee nameee 3217151 Sep  5  2005 04_Castelul_regelui_Arthur.dcr
-rwxrwxrwx 1 nameee nameee 3499415 Sep  5  2005 05_Curtea_palatului_Shogunului.dcr
-rwxrwxrwx 1 nameee nameee 2467518 Sep 13  2005 06_Palatul_Shogunului.dcr
-rwxrwxrwx 1 nameee nameee 1958627 Sep  5  2005 07_Incaperea_Shogunului.dcr
-rwxrwxrwx 1 nameee nameee 1930243 Sep  5  2005 08_Holul_Templului.dcr
-rwxrwxrwx 1 nameee nameee 3397092 Sep  5  2005 09_Trei_probe.dcr
-rwxrwxrwx 1 nameee nameee 3350101 Sep  5  2005 10_Holul_Laboratorului.dcr
-rwxrwxrwx 1 nameee nameee 2949194 Sep  5  2005 11_Camera_de_cercetari.dcr
-rwxrwxrwx 1 nameee nameee 4089915 Sep  5  2005 game_loader.exe
-rwxrwxrwx 1 nameee nameee  105320 Sep  7  2005 obrazek.bmp
-rwxrwxrwx 1 nameee nameee  955850 Sep 12  2005 Tedi.exe
-rwxrwxrwx 1 nameee nameee    3262 Aug 21  2005 tedi.ico
-rwxrwxrwx 1 nameee nameee  107462 Sep 13  2005 uninstall.exe
```


Given by the name `obrazek.bmp` (Polish for "picture.bmp") we can assume that the game was made by a polish team.


I have never seen `.dcr` files

```bash
└─$ hexdump -C 01_Drumul_spre_castel.dcr | head -n 2
00000000  58 46 49 52 d4 07 57 00  4d 44 47 46 72 65 76 46  |XFIR..W.MDGFrevF|
00000010  0f 8a 01 01 8e 3a 09 38  2e 35 2e 31 23 31 30 34  |.....:.8.5.1#104|
```


> The hex sequence 58 46 49 52 spells XFIR in ASCII and serves as the little-endian magic number/file signature for Macromedia / Adobe Director compressed resource files (such as .dir, .dxr, or .drx files).
>
> AI response

Running `strings` on the first `.dcr` file reveals in one of the lines:
```
...
 2004 Grzegorz Ludorowski
...
```
Perhaps a copyright from the owner (UI/UX team).


Curious about the `'0$'` file 

```bash
└─$ file '$0'
$0: PC bitmap, Windows 3.x format, 135 x 258 x 24, resolution 2834 x 2834 px/m, cbSize 105320, bits offset 54

└─$ hexdump -C '$0' | head
00000000  42 4d 68 9b 01 00 00 00  00 00 36 00 00 00 28 00  |BMh.......6...(.|
```

> Older installer creators (like NSIS or Inno Setup) use temporary variable names like $0, $1, or $TEMP to hold the installer wizard's background image or side-banner while the setup program is running
>
> Ai response



> Tedi.exe (This is likely the Macromedia "Projector" that plays the .dcr files)
> 
> Ai response

So, by reading more about Macromedia Projector, shows that the game was made in [Macromedia Director](https://en.wikipedia.org/wiki/Macromedia_Director) 

