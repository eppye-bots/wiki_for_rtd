## Safe file writing/lockings

### Problem
-   ERP writes an in-house file; bots starts to read this before 
    the file is completely written. 
-   Bots writes file over FTP, but file is read before Bots
    finishes writing. Bots provides some options in channels to handle
    this.

### Ways to handle this

1.  Tmp-part file name: bots writes a filename, than renames the file.
    Example 1. In channel: filename is "myfilename\_*.edi.tmp",
    -   tmp-part is ".tmp"  
    -   Bots writes: "myfilename\_12345.edi.tmp"  
    -   Bots renames: "myfilename\_12345.edi"

2.  System lock: use system file locks for reading or writing edi
    files (windows, \*nix).

3.  Lock-file: Directory locking: if lock-file exists in directory,
    directory is locked for reading/writing. Both eader and writer should
    check for this.
