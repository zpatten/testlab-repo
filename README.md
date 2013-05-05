# TestLab Example

This is all very much WIP.

If you are going to play with this; I would suggest cloning the `TestLab` and `LXC` gems to `vendor/checkouts` and `export GEMDEV=1`.  Chasing the `master` branch is the way to go for now.

* https://github.com/zpatten/testlab
* https://github.com/zpatten/lxc

If you want to see what is going on during all of this; open another terminal, locate the testlab.log file and proceed to tail it.

    [~/code/personal/testlab-repo] $ tl status && tl create && tl setup && tl status
    [TL] TestLab v0.3.1 Loaded

    NODES:
    +-----------+-------------------+-------------+---------+---------------+------+----------------------------+-----+-----+
    | ID        | INSTANCE_ID       | STATE       | USER    | IP            | PORT | PROVIDER                   | CON | NET |
    +-----------+-------------------+-------------+---------+---------------+------+----------------------------+-----+-----+
    | localhost | mytestlab-zpatten | not_created | vagrant | 192.168.13.37 | 22   | TestLab::Provider::Vagrant | 3   | 2   |
    +-----------+-------------------+-------------+---------+---------------+------+----------------------------+-----+-----+

    NETWORKS:
    You either have no networks defined or dead nodes!

    CONTAINERS:
    You either have no containers defined or dead nodes!
    [TL] TestLab v0.3.1 Loaded
    [TL] node localhost create                                   # Completed in 62.2860 seconds!
    [TL] TestLab v0.3.1 Loaded
    [TL] node localhost setup                                    # Completed in 60.8751 seconds!
    [TL] network east create                                     # Completed in 0.1008 seconds!
    [TL] network east up                                         # Completed in 0.1051 seconds!
    [TL] network west create                                     # Completed in 0.1008 seconds!
    [TL] network west up                                         # Completed in 0.1009 seconds!
    [TL] container server-east-1 create                          # Completed in 385.0663 seconds!
    [TL] container server-east-1 up                              # Completed in 0.4047 seconds!
    [TL] container server-east-1 setup                           # Completed in 18.1392 seconds!
    [TL] container server-west-1 create                          # Completed in 7.4557 seconds!
    [TL] container server-west-1 up                              # Completed in 0.3006 seconds!
    [TL] container server-west-1 setup                           # Completed in 17.5344 seconds!
    [TL] container chef-server create                            # Completed in 7.5597 seconds!
    [TL] container chef-server up                                # Completed in 0.4049 seconds!
    [TL] container chef-server setup                             # Completed in 13.9065 seconds!
    [TL] TestLab v0.3.1 Loaded

    NODES:
    +-----------+-------------------+---------+---------+---------------+------+----------------------------+-----+-----+
    | ID        | INSTANCE_ID       | STATE   | USER    | IP            | PORT | PROVIDER                   | CON | NET |
    +-----------+-------------------+---------+---------+---------------+------+----------------------------+-----+-----+
    | localhost | mytestlab-zpatten | running | vagrant | 192.168.13.37 | 22   | TestLab::Provider::Vagrant | 3   | 2   |
    +-----------+-------------------+---------+---------+---------------+------+----------------------------+-----+-----+

    NETWORKS:
    +-----------+------+---------+------------------+-----------+-------------+---------------+
    | NODE_ID   | ID   | STATE   | INTERFACE        | NETWORK   | NETMASK     | BROADCAST     |
    +-----------+------+---------+------------------+-----------+-------------+---------------+
    | localhost | east | running | br0:10.10.0.1/16 | 10.10.0.0 | 255.255.0.0 | 10.10.255.255 |
    | localhost | west | running | br1:10.11.0.1/16 | 10.11.0.0 | 255.255.0.0 | 10.11.255.255 |
    +-----------+------+---------+------------------+-----------+-------------+---------------+

    CONTAINERS:
    +-----------+---------------+---------+--------+---------+----------------------------------------------------+-----------------------------+
    | NODE_ID   | ID            | STATE   | DISTRO | RELEASE | INTERFACES                                         | PROVISIONER                 |
    +-----------+---------------+---------+--------+---------+----------------------------------------------------+-----------------------------+
    | localhost | server-east-1 | running | ubuntu | precise | east:eth0:10.10.0.254/16                           | TestLab::Provisioner::Shell |
    | localhost | server-west-1 | running | ubuntu | precise | west:eth0:10.11.0.254/16                           | TestLab::Provisioner::Shell |
    | localhost | chef-server   | running | ubuntu | precise | east:eth0:10.10.0.200/16, west:eth1:10.11.0.200/16 | TestLab::Provisioner::Shell |
    +-----------+---------------+---------+--------+---------+----------------------------------------------------+-----------------------------+
    [~/code/personal/testlab-repo] $
