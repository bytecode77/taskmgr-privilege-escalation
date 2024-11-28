# TaskMgr Volatile Environment LPE

| Exploit Information |                                   |
|:------------------- |:--------------------------------- |
| Date                | 28.10.2017                        |
| Patched             | Windows 10 RS3 (16299)            |
| Tested on           | Windows 8-10, x86 and x64         |

## Description

In taskmgr.exe, there is a DLL loading vulnerability that can be exploited by injecting an environment variable.

A load attempt to %SYSTEMROOT%\System32\srumapi.dll and various other DLL's will be performed from this auto-elevated process on Windows 10. In Windows 8, shell32.dll will be loaded.

Redirecting %SYSTEMROOT% can be achieved through Volatile Environment. For this, we set HKEY_CURRENT_USER\Volatile Environment\SYSTEMROOT to a new directory, which we then populate with our hijacked payload DLL, along with *.clb files from C:\Windows\Registration as they are loaded from our new directory as well.

Then, as we execute taskmgr.exe, it will load our payload DLL and on Windows 8 it will also load the COM+ components. We need to copy those, too, because the process will otherwise crash. I have included them for Windows 10, too, even though they are not currently required.

Our DLL is now executed with high IL. In this example, Payload.exe will be started, which is an exemplary payload file displaying a MessageBox.

## Expected Result

When everything worked correctly, Payload.exe should be executed, displaying basic information including integrity level.

![](https://bytecode77.com/images/pages/taskmgr-privilege-escalation/result.webp)

## Downloads

Compiled binaries with example payload:

[![](http://bytecode77.com/public/fileicons/zip.png) TaskMgrVolatileEnvironmentLPE.zip](https://downloads.bytecode77.com/TaskMgrVolatileEnvironmentLPE.zip)
(**ZIP Password:** bytecode77)

## Project Page

[![](https://bytecode77.com/public/favicon16.png) bytecode77.com/taskmgr-privilege-escalation](https://bytecode77.com/taskmgr-privilege-escalation)