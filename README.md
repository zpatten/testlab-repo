# TestLab Example

This is all very much WIP.

If you are going to play with this; I would suggest cloning the `TestLab` and `LXC` gems to `vendor/checkouts` and `export GEMDEV=1`.  Chasing the `master` branch is the way to go for now.

* https://github.com/zpatten/testlab
* https://github.com/zpatten/lxc

If you want to see what is going on during all of this; open another terminal, locate the testlab.log file and proceed to tail it.

    $ LOG_LEVEL=DEBUG be ./bin/tl-console
      GEMDEV:                          testlab, {:path=>"vendor/checkouts/testlab"}
      GEMDEV:                              lxc, {:path=>"vendor/checkouts/lxc"}
      GEMDEV:                              ztk, {:path=>"vendor/checkouts/ztk"}
      GEMDEV:                          testlab, {:path=>"vendor/checkouts/testlab"}
      GEMDEV:                              lxc, {:path=>"vendor/checkouts/lxc"}
      GEMDEV:                              ztk, {:path=>"vendor/checkouts/ztk"}

    From: /home/zpatten/code/testlab-repo/bin/tl-console @ line 14 :

         9: ui = ZTK::UI.new(:logger => logger) # ui interface class
        10: l = TestLab.new(:ui => ui)          # lab
        11: n = l.nodes.first                   # node
        12: c = n.containers.first              # container
        13: lxc = n.lxc                         # node lxc controller
     => 14: binding.pry

    [1] pry(main)> l.create
    => [:running]
    [2] pry(main)> l.status
    NODES:
    +-----------+-------------------+---------+---------+---------------+------+----------------------------+-----+-----+-----+
    | ID        | INSTANCE_ID       | STATE   | USER    | IP            | PORT | PROVIDER                   | CON | NET | RTR |
    +-----------+-------------------+---------+---------+---------------+------+----------------------------+-----+-----+-----+
    | localhost | mytestlab-zpatten | running | vagrant | 192.168.33.10 | 22   | TestLab::Provider::Vagrant | 3   | 2   | 1   |
    +-----------+-------------------+---------+---------+---------------+------+----------------------------+-----+-----+-----+

    NETWORKS:
    +-----------+------+---------+------------------------+
    | NODE_ID   | ID   | STATE   | INTERFACE              |
    +-----------+------+---------+------------------------+
    | localhost | east | stopped | br0:192.168.255.254/16 |
    | localhost | west | stopped | br1:10.255.255.254/8   |
    +-----------+------+---------+------------------------+

    CONTAINERS:
    +-----------+---------------+---------+--------+---------+----------------------------------------------------+-------------+
    | NODE_ID   | ID            | STATE   | DISTRO | RELEASE | INTERFACES                                         | PROVISIONER |
    +-----------+---------------+---------+--------+---------+----------------------------------------------------+-------------+
    | localhost | server-east-1 | stopped | ubuntu | precise | east:eth0:192.168.0.254/16                         |             |
    | localhost | server-west-1 | stopped | ubuntu | precise | west:eth0:10.0.0.254/8                             |             |
    | localhost | chef-server   | stopped | ubuntu | precise | west:eth0:10.0.0.200/8, east:eth1:192.168.0.200/16 |             |
    +-----------+---------------+---------+--------+---------+----------------------------------------------------+-------------+
    => true
    [3] pry(main)> l.up
    => [:running]
    [4] pry(main)> l.status
    NODES:
    +-----------+-------------------+---------+---------+---------------+------+----------------------------+-----+-----+-----+
    | ID        | INSTANCE_ID       | STATE   | USER    | IP            | PORT | PROVIDER                   | CON | NET | RTR |
    +-----------+-------------------+---------+---------+---------------+------+----------------------------+-----+-----+-----+
    | localhost | mytestlab-zpatten | running | vagrant | 192.168.33.10 | 22   | TestLab::Provider::Vagrant | 3   | 2   | 1   |
    +-----------+-------------------+---------+---------+---------------+------+----------------------------+-----+-----+-----+

    NETWORKS:
    +-----------+------+---------+------------------------+
    | NODE_ID   | ID   | STATE   | INTERFACE              |
    +-----------+------+---------+------------------------+
    | localhost | east | running | br0:192.168.255.254/16 |
    | localhost | west | running | br1:10.255.255.254/8   |
    +-----------+------+---------+------------------------+

    CONTAINERS:
    +-----------+---------------+---------+--------+---------+----------------------------------------------------+-------------+
    | NODE_ID   | ID            | STATE   | DISTRO | RELEASE | INTERFACES                                         | PROVISIONER |
    +-----------+---------------+---------+--------+---------+----------------------------------------------------+-------------+
    | localhost | server-east-1 | running | ubuntu | precise | east:eth0:192.168.0.254/16                         |             |
    | localhost | server-west-1 | running | ubuntu | precise | west:eth0:10.0.0.254/8                             |             |
    | localhost | chef-server   | running | ubuntu | precise | west:eth0:10.0.0.200/8, east:eth1:192.168.0.200/16 |             |
    +-----------+---------------+---------+--------+---------+----------------------------------------------------+-------------+
    => true
    [5] pry(main)> TestLab::Container.first("chef-server").ssh.console
    10.0.0.200
    ubuntu@10.0.0.200's password:
    Welcome to Ubuntu 12.04.2 LTS (GNU/Linux 3.2.0-23-generic x86_64)

     * Documentation:  https://help.ubuntu.com/

    The programs included with the Ubuntu system are free software;
    the exact distribution terms for each program are described in the
    individual files in /usr/share/doc/*/copyright.

    Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
    applicable law.

    ubuntu@chef-server:~$ ifconfig -a
    eth0      Link encap:Ethernet  HWaddr 00:00:5e:5b:e9:96
              inet addr:10.0.0.200  Bcast:10.255.255.255  Mask:255.0.0.0
              inet6 addr: fe80::200:5eff:fe5b:e996/64 Scope:Link
              UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
              RX packets:82 errors:0 dropped:0 overruns:0 frame:0
              TX packets:72 errors:0 dropped:0 overruns:0 carrier:0
              collisions:0 txqueuelen:1000
              RX bytes:15353 (15.3 KB)  TX bytes:13633 (13.6 KB)

    eth1      Link encap:Ethernet  HWaddr 00:00:5e:c8:5f:42
              inet addr:192.168.0.200  Bcast:192.168.255.255  Mask:255.255.0.0
              inet6 addr: fe80::200:5eff:fec8:5f42/64 Scope:Link
              UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
              RX packets:30 errors:0 dropped:0 overruns:0 frame:0
              TX packets:8 errors:0 dropped:0 overruns:0 carrier:0
              collisions:0 txqueuelen:1000
              RX bytes:7020 (7.0 KB)  TX bytes:636 (636.0 B)

    lo        Link encap:Local Loopback
              inet addr:127.0.0.1  Mask:255.0.0.0
              inet6 addr: ::1/128 Scope:Host
              UP LOOPBACK RUNNING  MTU:16436  Metric:1
              RX packets:2 errors:0 dropped:0 overruns:0 frame:0
              TX packets:2 errors:0 dropped:0 overruns:0 carrier:0
              collisions:0 txqueuelen:0
              RX bytes:202 (202.0 B)  TX bytes:202 (202.0 B)

    ubuntu@chef-server:~$
