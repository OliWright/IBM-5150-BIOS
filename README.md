# IBM 5150 BIOS

Reconstructed source for lots of early PC BIOSes can be found [here](https://sites.google.com/site/pcdosretro/ibmpcbios).

In order to assemble one of these BIOSes, you'll require an old assembler (MASM 4.0 or earlier) and you'll need to make some modifications to the source code.  That can be problematic for those of us at nerd level 23 or below.  This project is a modified 5150 V2 BIOS (U33 5700671 19th October 1981) that can be assembled using [uasm](http://www.terraspace.co.uk/uasm.html), which is a free modern assembler.  You can use this as a starting point for further modifications.

To assemble the BIOS, use the following command

```uasm64.exe -0 -bin -Fl PCBIOSV2.asm```

* `-0` indicates that we'd like `8086` code to be generated.
* `-bin` indicates that we'd like raw binary output.
* `-Fl` is entirely optional, it indicates that we'd like a listing file generated, which is handy.

The modifications to the source code have been carefully chosen so as to minimise the differences in the final binary, compared to the original ROM.  UASM is able to make some `jmp` instructions use a byte-relative mode, whereas the original ROM used a 16-bit offset.  In those cases, I've added a `nop` to re-align the code.  This makes diffing the dissasembly, or the binary less painful.

I also disabled the ROM checksum, because without an additional script to poke a checksum into the binary, the ROM will insta-halt.
