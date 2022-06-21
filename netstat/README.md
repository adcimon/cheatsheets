# netstat

[Netstat](https://en.wikipedia.org/wiki/Netstat) is a command-line network utility that displays network connections, routing tables, network interfaces and network protocol statistics.

List all connections.
```
netstat
netstat -a
```

List TCP connections.
```
netstat -at
```

List UDP connections.
```
netstat -au
```

List listening TCP ports.
```
netstat -lt
```

List listening UDP ports.
```
netstat -lu
```

Display statistics.
```
netstat -s
```

Display TCP statistics.
```
netstat -st
```

Display UDP statistics.
```
netstat -su
```

Display domain name for IP addresses.
```
netstat -F
```

Display only IP addresses.
```
netstat -n
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
