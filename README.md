# IBM 5150 BIOS

When working with an old computer like the original IBM PC, sometimes the original BIOS can be unhelpful in diagnosing problems.  At times it is very helpful if you're able to modify the code in some way.  This project builds on a project that [reconstructed the original source code](https://sites.google.com/site/pcdosretro/ibmpcbios) by allowing that code to be assembled with a modern assembler ([uasm](http://www.terraspace.co.uk/uasm.html)).

The BIOS in this project currently is a modified 5150 V2 BIOS (U33 5700671 19th October 1981).  The modifications here should hopefully allow similar modifications to be made to other versions if required.

To assemble the BIOS, use the following command

```uasm64.exe -0 -bin -Fl PCBIOSV2.asm```

* `-0` indicates that we'd like `8086` code to be generated.
* `-bin` indicates that we'd like raw binary output.
* `-Fl` is entirely optional, it indicates that we'd like a listing file generated, which is handy.

The modifications to the source code have been carefully chosen so as to minimise the differences in the final binary, compared to the original ROM.  UASM is able to make some `jmp` instructions use a byte-relative mode, whereas the original ROM used a 16-bit offset.  In those cases, I've added a `nop` to re-align the code.  This makes diffing the dissasembly, or the binary less painful.

I also disabled the ROM checksum, because without an additional script to poke a checksum into the binary, the ROM will insta-halt.

All the diffs made to the source code can be seen [here](https://github.com/OliWright/IBM-5150-BIOS/compare/f8df3606aceb9b5ae06ebc1d41cc239c37660d66...44b7705f4625770eb21594673b094d5d4f948ec5)
