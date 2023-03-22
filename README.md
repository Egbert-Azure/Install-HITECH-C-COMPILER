# INSTALLING THE UPDATED HITECH-C COMPILER FOR CP/M ON GenieIIIs Computer

Our objective is to run the updated C compiler on real Genie III or sdltrs emulator. Next step would be to build a cross compiler on Windows with Visual Studio.

**NOTE:**  updates and enhancements to the HI-TECH C Compiler for Z80 v3.09 running are available on from this site:
<https://github.com/agn453/HI-TECH-Z80-C>

The latest release is V3.09-16

The HI-TECH Z80 CP/M C compiler v3.09 is provided free of charge for any use, private or commercial, strictly as-is. No warranty or product support is offered or implied. You may use this software for whatever you like, providing you acknowledge that the copyright to this software remains with HI-TECH Software.
The dist folder contains the entire compiler including the original distributed library source-code in Huffman-encoded archive files (CPM.HUF, GEN.HUF, FLOAT.HUF and STDIO.HUF). NB: I have not rebuilt the .HUF files - so please use updated run-time library source files in the following folders.
The cpm, gen, float and stdio folders contain the library source-code that has been extracted from the .HUF archive files using DEHUFF.COM and the updated/modified files. The doc folder contains the documentation in ASCII text as HTCZ80.TXT.

## Installing the patched & updated HITECH-C compiler
Download htc-bin.lbr from the git repo, and transfer to CP/M 3 machine or emulator.

The lbr format can be upacked with `NULU.COM` or `LBREXT.COM`

Run e.g. `p:lbrext c9:htc-bin.lbr c9:` - (change the drive letter/user as they apply to your system)

Download `testtrig.c` from the repo or here.

`c309.com` is the patched and updated compiler for 8-bit system

Compile using `c309 -o -lf testtrig.c`and run `testtrig.com`

![Screenshot 2023-03-21 201501](https://user-images.githubusercontent.com/55332675/226792943-b155e17f-1d28-4ed8-b40a-50a34d8d68ac.jpg)

You should rename `C309.COM` to `C.COM` with pip `C.COM=C309.COM`

Add a file `ENVIRON.` in your Hitech user area and your working area:
![Screenshot 2023-03-21 201502](https://user-images.githubusercontent.com/55332675/226793998-eac932a1-6a7e-47b3-a807-ea05b31090a8.jpg)

