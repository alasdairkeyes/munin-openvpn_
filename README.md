# munin-openvpn_
OpenVPN plugin for munin (Yet another one)

# Name

openvpn_ - Plugin to monitor the OpenVPN server on a system

# Configuration

This script can generate various graphs for OpenVPN servers.


First, ensure that your OpenVPN install is writing out statistics.
To find the file used search for the status in your config

```
  # grep 'status ' /etc/openvpn/server.conf
  status openvpn-status.log
```

If the line doesn't exist, add it in and restart the OpenVPN service.
This usually makes the status file's full path as /etc/openvpn/openvpn-status.log


Update your Munin plugins config to include the following. By default
the script will try to read /etc/openvpn/openvpn-status.log if no 
env.openvpn_status_file entry exists

```
[openvpn_*]
  user root
  env.openvpn_status_file /etc/openvpn/openvpn-status.log
```

Place/symlink openvpn_ into your Munin plugin area (Usually /usr/share/munin/plugins/)


To list the graphs available run

```
  $ ./openvpn_ suggest
```

This is also provided as part of munin-node-configure
```
  # munin-node-configure --suggest
  openvpn_                   | no   | yes (+connected_users +total_traffic)
```

```
  # munin-node-configure --suggest --shell
  ln -s '/usr/share/munin/plugins/openvpn_' '/etc/munin/plugins/openvpn_connected_users'
  ln -s '/usr/share/munin/plugins/openvpn_' '/etc/munin/plugins/openvpn_total_traffic'
```

Setup the symlinks and restart munin-node service

# Dependencies

This is written in Perl, install required dependencies via package manager

- YUM (Redhat/CentOS)

```
yum install perl-DateTime
```

- APT (Debian/Ubuntu)

```
apt-get install libdatetime-perl
```

# Version

0.1

# Site

https://github.com/alasdairkeyes/munin-openvpn_

# Author

Alasdair Keyes - https://akeyes.co.uk/

# License

GPLv3 - See LICENSE file

