# tcpdump

<p align="center"><img align="center" src="assets/tcpdump.png"></p>

[tcpdump](https://www.tcpdump.org/) is a powerful command-line packet analyzer.

IP traffic.
```
tcpdump host 1.1.1.1
tcpdump src 1.1.1.1
tcpdump dst 1.1.1.1
```

Port traffic.
```
tcpdump port 1234
tcpdump src port 1234
tcpdump dst port 1234
tcpdump portrange 8080-9090
```

Protocol traffic.
```
tcpdump udp
```

Network traffic.
```
tcpdump net 1.2.3.0/24
```

IP6 traffic.
```
tcpdump ip6
```

Interface traffic.
```
tcpdump -i eth0
```

Writing and reading to a file.
```
tcpdump -w file.txt
tcpdump -r file.txt
```

Conditions.
```
and
or
not
```

Options.
```
-q Quiet
-v Verbose
```
