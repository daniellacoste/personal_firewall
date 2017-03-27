# :fire: personal_firewall :fire:
A program that emulates a personal firewall (specific to IPv4 packets), written in Python.

__Pre-reqs__: Python3

This firewall is capable of filtering both incoming and outgoing packets. For simplicity, there is no networking involved - future versions may include network capabilities. The program simply reads in a specified config file, reads packets from stdin, and outputs the results to stdout.

When the simulator starts, it first reads in the firewall rules via the config file. After reading in the rules, the simulator will then start reading standard input line by line. Each line via standard input will describe a simulated packet. For each packet, the program determines what action to incur on the packet based on the rules in the config file. The resulting actions are sent to stdout.

### Configuration file format:

``` 
<direction> <action> <ip> <port> [flag]
```

* __direction__: the direction of the traffic, 'in' or 'out'
* __action__: what to do with the packet, 'accept', 'drop', and 'deny'
* __ip__: defines the IP range, specified by an IP range using CIDR notation, or a wildcard '*'
* __port__: a destination port which is an integer b/w 0-65535, comma delimited, wildcard '*' available
* __flag__: (optional) "established" flag which describes whether the rule will be applied only to packets that are part of an established connection or to all packets (if the field is not present, the rule applies to all packets)

### Packet file format:

```
<direction> <ip> <port> <flag>
```

* __direction__: direction of the packet - either 'in' or 'out'
* __ip__: for incoming packets this is the source IP address, for outgoing packets this is the destination IP address
* __port__: integer b/w 0-65535
* __flag__: boolean 0 (new session) or 1 (established session)

### Output:

```
<action>(<rule number>) <direction> <ip> <port> <flag>
```

*Written for W2017 CPSC 526: Network Security*
