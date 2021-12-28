# hfuzz_toolkit

Utility scripts for working with honggfuzz


### `hf_uniq_pc <workspace_dir>`
Given a workspace directory, lists the unique PCs where crashes have occurred


### `hf_smallest_crash <workspace_dir>`
For each unique PC, list the smallest input file crashing at that PC


### `hf_source_of_crash <workspace_dir> <executable> [arguments]`
**Warning:** This script is fragile, and only works if you compiled your binary with hfuzz-clang

For a workspace dir or single input file, find the source code line
in the executable (uses `addr2line` from binutils) closest to the crash.

For example, if the crash PC is in `strdup()`, the library code will be
ignored and the script will list the application's call to that function.

```
albin@KNYTT:haxlib$ hf_source_of_crash findings_dbf ./fuzz.bin ___FILE___
/home/albin/fuzz/haxlib/src/haxopen.c:1234
/home/albin/fuzz/haxlib/src/api.c:12
```

Each listing refers to one crashing input file.

```
albin@KNYTT:haxlib$ hf_source_of_crash findings_dbf/SIGSEGV.xyz.fuzz ./fuzz.bin ___FILE___
/home/albin/fuzz/haxlib/src/haxopen.c:1234
```


