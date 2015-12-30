# Gateway Setting

This comes from another project that currently I use, it's a VPN server that configure to connect to another VPN and 
set the routing table to control the traffic flow.

## Problem
Basically, I use VPN for controlling the traffic I serve on internet. So when I connect to my VPN server, inside the server 
will have a routing table that route the packet to specific place e.g. request to access private server A that requires
VPN B to access need to route to this specific tunnel.

All the software on Linux is already done and well made e.g. IPTable, Open VPN, PPTP Client so we don't need to build all
this again, what's the problem is all this tools manage by the configuration file and command line settings. So to change
some routing or adding a new VPN, need to create a new configure and restart the service to make it available but after
VPN is connected and routing table is defined everything is rarely to change.

One another case that might be a plus is internal DNS that can define the route of domain. So when enter website that need
to testing, just configure the DNS and route and everything is done.

## Solution
The UI with access control and routing table configuration with DNS setting as a plus.
