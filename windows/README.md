# Windows

<p align="center"><img align="center" width="20%" height="20%" src="assets/windows.svg"></p>

[Windows](https://www.microsoft.com/windows/) is a group of several proprietary graphical operating system families developed and marketed by [Microsoft](https://www.microsoft.com/).

## Index

* [Shell](#shell)
* [File System](#file-system)

## Shell

| Command                  | Description                                                                          |
|--------------------------|--------------------------------------------------------------------------------------|
| cd                       | Change directory.                                                                    |
| cls<br>clear             | Clear the console.                                                                   |
| dir<br>ls                | List files and directories.                                                          |
| dir env:<br>ls env:      | List the environment variables.                                                      |
| set                      | Set an environment variable.                                                         |
| scp -r file user@ip:path | Secure copy files or directories between 2 computers.                                |
| systeminfo               | Displays detailed configuration information about the computer and operating system. |
| $env:name="value"        | Set an environment variable.                                                         |

PowerShell script `ps1` cannot be loaded because running scripts is disabled on this system.
* Run PowerShell as administrator by clicking "Run as Administrator".
* Get the current execution policy with the command `Get-ExecutionPolicy`, the value would be `Restricted`.
* Set the execution policy with the command `Set-ExecutionPolicy RemoteSigned` and type "Y".

PowerShell redirect `stdin` and `stdout`.
```
Get-Content input.txt | program.exe > output.txt
Start-Process "program.exe" -RedirectStandardInput "input.txt" -RedirectStandardOutput "output.txt" -NoNewWindow -Wait
```

## File System

Hosts file maps human-friendly hostnames to numerical Internet Protocol (IP) addresses.
```
C:\Windows\System32\Drivers\etc\hosts
```
