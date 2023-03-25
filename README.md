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

Implement Hi-Tech Cross compiler for Windows with Visual Studio.
To compile and also run Z80 CP/M programs with Windows Mark Ogden's "one click" solution to install `zxc`is highly recommended.

Details can be found here
<https://raw.githubusercontent.com/agn453/ZXCC/main/winbuild/README.md>

1. If you don’t already have visual studio installed, install the community edition, which is free from Microsoft.
2. Clone the repository `zxcc` repository from github into an area of your choice.
3. Modify the `install.cfg` script in the winbuild sub directory to reflect where you want the final files to be installed, the sample file has the install path as `d:\bin`, change to match your local requirements
4. Open the solution file `wzxcc.sln` file in the winbuild directory with `Visual Studio` or `Visual Studio Cod`e and build the solution you want. X64 Release is default, if you are running on a 32bit version of Windows you need to switch to X32.
![image](https://user-images.githubusercontent.com/55332675/227419477-6e783754-d7ef-4dea-87a9-66f4f756df7f.png)

5. Install the hitech C compiler from the github website  <https://github.com/agn453/HI-TECH-Z80-C> on your Z80 system (in my case the Genie IIIs) and copy the needed files also to the Windows `zx`c subdirectories.

`zxcc` uses three directories:

* `BINDIR80` (by default, ...\bin80) holds the compiler itself.
       You should copy the compiler .com files (or MAC, RMAC etc.)
       and bios.bin to this directory.
* `LIBDIR80` (by default, ... \lib80) holds the C
       libraries libc.lib, libf.lib, crtcpm.obj and rrtcpm.obj.
* `INCDIR80` (by default, ... \include80) holds the
       compiler .h files.

Copy the necessary files into the directory. For the Genie IIIs with Holte CP/M, copy `HOLTE.LIB` into `bin80` too.

>Only the location for zxc is set by the configure script under Windows; you can override them by editing zxcc.h and uncommenting the lines that redefine them and re-compile.

Mark created a simplified option to set `CPMDIR80` to point to the `zxc` binary directory, but you need to create the subdirectories `bin80`, `lib80` and `include80`.

Create and set the environment variable `CPMDIR80`via the control panel. That way, it will also point to the subdirectories:

``` console
{CPMDIR80}\bin80

{CPMDIR80}\lib80

{CPMDIR80}\include80
```

Once you have installed `zxc` and the build tools, try building HelloWorld opening a terminal within Visual Studio:

``` c
#include <stdio.h>
  void main()
     {
     printf("Hello World\n");
     }
```

Then compile and run it.

![image](https://user-images.githubusercontent.com/55332675/227382323-a97b2943-031d-4a71-9272-fd52d08bd218.png)

You are good to go. After creating and filling the cross-compiler directories and defining the INCDIR80, LIBDIR80 and PATH environment variables, you can compile your source programs in any current directory using the `zxc` control program with the necessary options and a list of processed programs.

![image](https://user-images.githubusercontent.com/55332675/227391414-3cc54518-46ac-4773-9db1-b9a5c05e5844.png)

Within Visual Studio Code you should define `tasks.json`

``` json
{
    "version": "2.0.0",
    "tasks": [
        {
            "type": "shell",
            "label": "C: zxc build active file",
            "command": "zxc",
            "args": [
                "${file}",
                "-lf"
            ],
            "group": {
                "kind": "build",
                "isDefault": true
            }
        }
    ]
}
```

And `settings.json` associated with the c file ending:

``` json
{
    "files.associations": {
        "*.c": "zxc"
    }
}
```

This should make it the default build task that runs when you press `Ctrl+Shift+B`.
Default is `libz.lib` which needs to be changed depending on your project.

## Acknowledgments ##

Thank you to HI-TECH SOFTWARE for writing the Hi-Tech C v3.09 compiler for CP/M and allowing free use of it.

Thanks to John Elliott for writing the zxcc emulator.

Thanks to Mark Ogden for his amazing work to create a simplified solution for Windows cross compiler.

I'm thankful to all the unnamed people who cared enough to restore and preserve information about this wonderful compiler and the CP/M operating system.

I apologize if I forgot to mention anyone.
