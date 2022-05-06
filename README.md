# wl-recompile-experiment

wl is driver for broadcom wireless chips

driver is not compatible with other kernel version so driver needs to be compiled again if kernel changes

so broadcom provides dkms source with closed source blobs included which includes blobs only for i386 and amd64

i came up with an idea to convert i386 blob to llvm bitcode using retdec since retdec was the only decompiler i was reasonably accessible

and then compile llvm bc to arm using llc

```
retdec-decompiler wlc_hybrid.o_i386
llc -filetype=obj -mtriple=arm-linux-gnueabi (bc file).bc
```

`wlc_hybrid.o_i386` is original blob extracted from debian dkms package
`wlc_hybrid.o_i386.bc` is bitcode output from retdec
`wlc_hybrid.o_i386.o_armel` is binary recompiled using llc for armel
`wlc_hybrid.o_i386.o_armhf` is binary recompiled for armhf
