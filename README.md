# How to install updated HITECH-C Compiler CP/M - GenieIIIs Computer

Our objective is to run the updated C compiler on real Genie IIIs or sdltrs emulator. Next step would be to build a cross compiler on Windows with Visual Studio.

**NOTE:**  updates and enhancements to the HI-TECH C Compiler for Z80 v3.09 running are available on from this site:
<https://github.com/agn453/HI-TECH-Z80-C>

The latest release is V3.09-16

The HI-TECH Z80 CP/M C compiler v3.09 is provided free of charge for any use, private or commercial, strictly as-is. No warranty or product support is offered or implied. You may use this software for whatever you like, providing you acknowledge that the copyright to this software remains with HI-TECH Software.
The dist folder contains the entire compiler including the original distributed library source-code in Huffman-encoded archive files (CPM.HUF, GEN.HUF, FLOAT.HUF and STDIO.HUF).

The cpm, gen, float and stdio folders contain the library source-code that has been extracted from the .HUF archive files using DEHUFF.COM and the updated/modified files. The doc folder contains the documentation in ASCII text as HTCZ80.TXT.

## Installing the patched & updated HITECH-C compiler

Download `htc-bin.lbr` from the git repo, and transfer to CP/M 3 machine or emulator.

The lbr format can be upacked with `NULU.COM` or `LBREXT.COM`

Run e.g. `p:lbrext c9:htc-bin.lbr c9:` - (change the drive letter/user as they apply to your system)

Download `testtrig.c` from the repo or here.

`c309.com` is the patched and updated compiler for 8-bit system

Compile using `c309 -o -lf testtrig.c`and run `testtrig.com`

![Screenshot 2023-03-21 201501](https://user-images.githubusercontent.com/55332675/226792943-b155e17f-1d28-4ed8-b40a-50a34d8d68ac.jpg)

You should rename `C309.COM` to `C.COM` with pip `C.COM=C309.COM`

Add a file `ENVIRON.` in your Hitech user area and your working area:

![Screenshot 2023-03-21 201502](https://user-images.githubusercontent.com/55332675/226793998-eac932a1-6a7e-47b3-a807-ea05b31090a8.jpg)

## Z3PLUS

To run Hitech-C compiler within `Z3PLUS` you need to switch to `z3plus small` and then run commands like:

`alias.cmd`:

ALIASES to make it easier to access the HI-TECH-C Compiler located in C9:HITECH. The sources of the C-programs are supposed to be located in another user area, namely in C11:CSOUR. Before LIBC.LIB, HOLTE.LIB for Genie IIIs is searched. The parameter -lz is used to include LIBZ.LIB!

Where cc initiates a normal compiler run and ccf is intended for programs with floating-point numbers.

```console
CN z3plus small;C9:C -i9:c: $1.c 9:c:libc.lib $-1 -lz;z3plus

CC z3plus small;C9:C -i9:c: $1.c 9:c:holte.lib $-1 -lz;z3plus

CCF z3plus small;C9:C -i9:c: $1.c 9:c:holte.lib $-1 -lf -lz;z3plus
```

Search for expression

``` console
grep c9:grep $*
```

Start C-PreCompiler for syntax-check

```console
pre hitech:pcc $*
```

![Screenshot 2023-03-21 201503](https://user-images.githubusercontent.com/55332675/226808221-ece5623b-1156-44f2-9960-690e50548c31.jpg)

## Creating a cross compiler for Windows

(WIP)

Implement Hi-Tech Cross compiler for Windows with Visual Studio

** DRAFT NOTES: ** 

https://raw.githubusercontent.com/agn453/ZXCC/main/winbuild/README.md

zxcc uses three directories:

     * BINDIR80 (by default, ...\bin80) holds the compiler
       itself. You should copy the compiler .com files (or MAC, RMAC etc.)
       and bios.bin to this directory.
       
     * LIBDIR80 (by default, ... \lib80) holds the C
       libraries libc.lib, libf.lib, crtcpm.obj and rrtcpm.obj.
       
     * INCDIR80 (by default, ... \include80) holds the
       compiler .h files.
     
     * Only the location for zxc is set by the configure script under Windows;
       you can override them by editing zxcc.h and uncommenting the lines that redefine them and re-compile
    


![image](https://user-images.githubusercontent.com/55332675/227382323-a97b2943-031d-4a71-9272-fd52d08bd218.png)


![image](https://user-images.githubusercontent.com/55332675/227391414-3cc54518-46ac-4773-9db1-b9a5c05e5844.png)
