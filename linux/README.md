# Linux

<p align="center"><img align="center" width="20%" height="20%" src="assets/linux.svg"></p>

[Linux](https://www.linux.org/) is a family of open-source Unix-like operating systems based on the Linux kernel.

## Environment Variables

Environment variable with command scope.
```
FOO=bar command
FOO=bar; command
```

```
export FOO=bar
command
unset FOO
```

Environment variable with terminal scope.
```
export FOO=bar
command0
command1
...
```

## Commands

| Command                  | Description                                           |
|--------------------------|-------------------------------------------------------|
| cd                       | Change directory.                                     |
| clear                    | Clear the console.                                    |
| ls<br>ls -l<br>ls -a     | List files and directories.                           |
| lsb_release -d           | Show Ubuntu version.                                  |
| mpstat -P ALL            | Monitor CPU.                                          |
| nvidia-smi               | Monitor NVIDIA GPU.                                   |
| ps<br>ps -aux            | Show processes.                                       |
| ps -aef --forest         | Show the tree of processes.                           |
| scp -r file user@ip:path | Secure copy files or directories between 2 computers. |
| shutdown -h now          | Shutdown the machine.                                 |
| sudo su -                | Switch to superuser.                                  |
| top                      | Monitor processes.                                    |
| watch -n interval        | Run command at regular intervals.                     |
