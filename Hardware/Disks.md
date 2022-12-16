# Disks

## Windows

### chkdsk

Fixes errors on the disk.

    chkdsk f: /F
    chkdsk f: /F /R /X

```
  /R                  Locates bad sectors and recovers readable information
                      (implies /F, when /scan not specified).
  /X                  Forces the volume to dismount first if necessary.
                      All opened handles to the volume would then be invalid
                      (implies /F).
  /X                  Forces the volume to dismount first if necessary.
                      All opened handles to the volume would then be invalid
                      (implies /F).
```
### DISM

    DISM.exe /Online /Cleanup-image /Restorehealth

```
  /Online                 - Targets the running operating system.
  /Cleanup-Image          - Performs cleanup and recovery operations on the
                            image.
  /Cleanup-Image {/CheckHealth | /ScanHealth | /RestoreHealth}
    Use /CheckHealth to check whether the image has been flagged as corrupted by a failed process and whether the corruption can be repaired.
    Use /ScanHealth to scan the image for component store corruption. 
    Use /RestoreHealth to scan the image for component store corruption, and then perform repair operations automatically. 
    Use /Source with /RestoreHealth to specify the location of known good versions of files that can be used for the repair. For more information on specifying a source location, see https://go.microsoft.com/fwlink/?LinkId=243077.
    Use /LimitAccess to prevent DISM from contacting WU/WSUS.

    Example:
      DISM.exe /Online /Cleanup-Image /ScanHealth

      DISM.exe /Image:c:\offline /Cleanup-Image /RestoreHealth
      /Source:c:\test\mount
```

### sfc

    sfc /scannow
    sfc /scannow /offbootdir=X:\ /offwindir=C:\Windows

```
/SCANNOW        Scans integrity of all protected system files and repairs files with problems when possible.
/OFFBOOTDIR     For offline repair, specify the location of the offline boot directory
/OFFWINDIR      For offline repair, specify the location of the offline windows directory
```

### format

Format with zeros

    format f: /fs:NTFS /p:0

```
  /FS:filesystem  Specifies the type of the file system (FAT, FAT32, exFAT,
                  NTFS, UDF, ReFS).
  /P:count        Zero every sector on the volume.  After that, the volume
                  will be overwritten "count" times using a different
                  random number each time.  If "count" is zero, no additional
                  overwrites are made after zeroing every sector.  This switch
                  is ignored when /Q is specified.
```

## Linux

### smartctl

Begin an extended self-test of drive `/dev/hdc`. You can issue this command on a running system. The results can be seen in the self-test log visible with the `-l selftest` option after it has completed. 

    smartctl -t long /dev/sdb




