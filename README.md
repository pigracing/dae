# dae

<img src="https://github.com/v2rayA/dae/blob/main/logo.png" border="0" width="25%">

***dae***, means goose, is a lightweight and high-performance transparent proxy solution.

In order to improve the traffic split performance as much as possible, dae runs the transparent proxy and traffic split suite in the linux kernel by eBPF. Therefore, we have the opportunity to make the direct traffic bypass the forwarding by proxy application and achieve true direct traffic through. Under such a magic trick, there is almost no performance loss and additional resource consumption for direct traffic.

As a successor of [v2rayA](https://github.com/v2rayA/v2rayA), dae abandoned v2ray-core to meet the needs of users more freely.

## Usage

Build:
```shell
git clone https://github.com/v2rayA/dae.git
cd dae
git submodule update --init
make
```

Run:
```shell
./dae run -c example.dae
```

See [example.dae](https://github.com/v2rayA/dae/blob/main/example.dae).

## Linux Kernel Requirement

### Kernel Version

Use `uname -r` to check the kernel version on your machine.

**Bind to LAN: >= 5.8**

You need bind dae to LAN interface, if you want to provide network service for LAN as an intermediate device.

This feature requires the kernel version of machine on which dae install >= 5.8.

Note that if you bind dae to LAN only, dae only provide network service for traffic from LAN, and not impact local programs.

**Bind to WAN: >= 5.8**

You need bind dae to WAN interface, if you want dae to provide network service for local programs.

This feature requires kernel version of the machine >= 5.8.

Note that if you bind dae to WAN only, dae only provide network service for local programs and not impact traffic coming in from other interfaces.

## TODO

1. Check dns upstream and source loop (whether upstream is also a client of us) and remind the user to add sip rule.
1. Domain routing performance optimization.
1. Handle the case that nodes do not support UDP by adding `filter: l4proto_out(tcp, udp)`, and filter out those nodes support both TCP and UDP. Thus we can use routing to handle it.
1. Handle the case that nodes do not support IPv6 by adding `filter: ipversion_out(4, 6)`, and filter out those nodes support both IPv4 and IPv6. Thus we can use routing to handle it.
1. L4Checksum problem. Maybe it is hard to solve.
1. MACv2 extension extraction.
1. Log to userspace.
1. ...
