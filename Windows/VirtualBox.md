# VirtualBox

## Start guest on os standard.

+ Open directory
`C:\Users\[user]\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup`
+ Create shortcut
  `Right click` -> `New` -> `Shortcut`
+ Set **Type the location of the item** to
`"C:\Program Files\Oracle\VirtualBox\VBoxManage.exe" startvm "vmname" --type headless`

  <font size="1">Adjust path to **VBoxManage.exe** if needed</font>
+ Set shortcut name

## Shutdown all VMs

Create simple batch script:

<font size="1">Adjust path to **VBoxManage.exe** if needed</font>
```batch
@ECHO OFF

SET what=savestate

IF [%1%] == [1] (
    SET what=poweroff
)

SET get_vm="C:\Program Files\Oracle\VirtualBox\VBoxManage.exe" list runningvms
FOR /F "tokens=1" %%V IN ('%get_vm%') DO (
     ECHO Shutting down %%V (%what%^)
     "C:\Program Files\Oracle\VirtualBox\VBoxManage.exe" controlvm %%V %what%
)
```