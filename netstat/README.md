# netstat

[Netstat](https://en.wikipedia.org/wiki/Netstat) is a command-line network utility that displays network connections, routing tables, network interfaces and network protocol statistics.

List all connections.
```
netstat
netstat -a
```

List TCP or UDP connections.
```
netstat -at
netstat -au
```

List listening TCP or UDP ports.
```
netstat -lt
netstat -lu
```

Display statistics.
```
netstat -s
```

Display TCP or UDP statistics.
```
netstat -st
netstat -su
```

Display connections with process PID.
```
netstat -o
```

Displays connections with the executable involved in creating each connection or listening port.
```
netstat -b
```

Show kernel's network routing table and information.
```
netstat -r
netstat -rn
```
