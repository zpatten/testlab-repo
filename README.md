# TestLab Example

This is all very much WIP.

If you are going to play with this; I would suggest cloning the `TestLab` and `LXC` to `vendor/checkouts` and `export GEMDEV=1`.

    $ be ./bin/tl-console
      GEMDEV:                          testlab, {:path=>"vendor/checkouts/testlab"}
      GEMDEV:                              lxc, {:path=>"vendor/checkouts/lxc"}
      GEMDEV:                              ztk, {:path=>"vendor/checkouts/ztk"}
      GEMDEV:                          testlab, {:path=>"vendor/checkouts/testlab"}
      GEMDEV:                              lxc, {:path=>"vendor/checkouts/lxc"}
      GEMDEV:                              ztk, {:path=>"vendor/checkouts/ztk"}

    From: /home/zpatten/code/testlab-repo/bin/tl-console @ line 14 :

         9: ui = ZTK::UI.new(:logger => logger) # ui interface class
        10: l = TestLab.new(ui)                 # lab
        11: n = l.nodes.first                   # node
        12: c = n.containers.first              # container
        13: lxc = n.lxc                         # node lxc controller
     => 14: binding.pry

    [1] pry(main)> l.create
    => [:running]
    [2] pry(main)> l.up
    => [:running]
    [3] pry(main)> l.status
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
    | localhost | server-east-1 | running | ubuntu | lucid   | east:eth0:192.168.0.254/16                         |             |
    | localhost | server-west-1 | running | ubuntu | precise | west:eth0:10.0.0.254/8                             |             |
    | localhost | chef-server   | running | ubuntu | precise | west:eth0:10.0.0.200/8, east:eth1:192.168.0.200/16 |             |
    +-----------+---------------+---------+--------+---------+----------------------------------------------------+-------------+
    => true
    [4] pry(main)> n.ssh.console
    Welcome to Ubuntu 12.04 LTS (GNU/Linux 3.2.0-23-generic x86_64)

     * Documentation:  https://help.ubuntu.com/
    Welcome to your Vagrant-built virtual machine.
    Last login: Thu Apr 25 01:18:02 2013 from 192.168.33.1
    vagrant@mytestlab-zpatten:~$
