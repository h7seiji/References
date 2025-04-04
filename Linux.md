# Linux

<https://www.brendangregg.com/linuxperf.html>

## Commands

- <https://blog.stackademic.com/advanced-linux-commands-for-the-modern-hacker-84b1cd4ca15f>
  - Netcat (`nc`)
  - tcpdump
  - nmap
  - chroot
  - strace
  - lsof
  - iptables
  - grep
  - sed & awk
  - find
  - cron

## iptables

Iptables is a firewall program for Linux. It uses tables of IP packet filter rules in the Linux kernel to monitor and filter traffic from and to your server. Each table contains a number of chains, which are lists of rules that can match a set of packets. When a packet matches a rule, it is given a target, which can be another chain or a special value.

## UFW - Uncomplicated Firewall

<https://help.ubuntu.com/community/UFW>

## tcpdump

The tcpdump command can be used to capture network traffic on a Linux system.

## File Permissions

```sh
chmod a+rx my-script.sh
chmod -R a+rx directory
```

## Shell commands

### Download and Unzip

```sh
curl -o sdk.zip https://partner.steamgames.com/downloads/steamworks_sdk_157.zip
unzip sdk.zip
```

### chroot

Changes the apparent root directory for the current running process and their children.
A program that is run in such a modified environment cannot access files and commands outside that environmental directory tree.
