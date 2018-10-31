# h_canal
Hyper Canal - abstraction over the network protocols

H_Canal structure:
Each H_Canal consists of flows. (Protocols - L1, L2...)
Each H_Canal has a Start and an End.
The Start and End should consist the same flows.
Flow can be Abstract form of "Any" this means any traffic of this protocol.

The Abstraction over the classical OSI model should give a vendor-free overview of the real network data flow
going across the devices.
Each protocol is represented as an abstract flow.


It observes the devices as "filters" and the filter can split/block/modify/aggregte canals.

 
Each device specifies which flows it filters. 
Device by default ignores the flows, it can't filter.

For example H_Canal:

Start:
Protocol IPv4 [src - 1.1.1.0/24
               dst - 2.2.2.0/24]
Protocol TCP [src - 1024-65000
              dst - Any]

End:
Protocol IPv4 [src - 1.1.1.0/24
               dst - 2.2.2.0/24]
Protocol TCP [src - 1024-65000
              dst - Any]

After being filtered by firewall.
The firwall has only 2 rules:
Any -> 2.2.2.2/32 : 80 permit
Any -> 2.2.2.2/32 : 443 permit (make a nat translation from 2.2.2.2/32-> 3.3.3.3/32)

Canals outpt:
#1
Start:
Protocol IPv4 [src - 1.1.1.0/24
               dst - 2.2.2.2/32]
Protocol TCP [src - 1024-65000
              dst - 80]

End:
Protocol IPv4 [src - 1.1.1.0/24
               dst - 2.2.2.2/32]
Protocol TCP [src - 1024-65000
              dst - 80]

#2
Start:
Protocol IPv4 [src - 1.1.1.0/24
               dst - 2.2.2.2/32]
Protocol TCP [src - 1024-65000
              dst - 443]

End:
Protocol IPv4 [src - 1.1.1.0/24
               dst - 3.3.3.3/32]
Protocol TCP [src - 1024-65000
              dst - 443]
