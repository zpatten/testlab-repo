[![Dependency Status](https://gemnasium.com/zpatten/testlab-repo.png)](https://gemnasium.com/zpatten/testlab-repo)

# TestLab Example

This is all very much WIP.

If you are going to play with this; I would suggest cloning the `TestLab` and `LXC` gems to `vendor/checkouts` and `export GEMDEV=1`.  Chasing the `master` branch is the way to go for now.

* https://github.com/zpatten/testlab
* https://github.com/zpatten/lxc

If you want to see what is going on during all of this; open another terminal, locate the testlab.log file and proceed to tail it.

    $ tl setup
    [TL] TestLab v0.5.4 Loaded
    [TL] node localhost create                                   # Completed in 2.4198 seconds!
    [TL] node localhost up                                       # Completed in 1.9134 seconds!
    [TL] node localhost setup                                    # Completed in 60.3821 seconds!
    [TL] network east create                                     # Completed in 0.1013 seconds!
    [TL] network east up                                         # Completed in 0.1011 seconds!
    [TL] network west create                                     # Completed in 0.1010 seconds!
    [TL] network west up                                         # Completed in 0.1012 seconds!
    [TL] container chef-server create                            # Completed in 0.1007 seconds!
    [TL] container chef-server up                                # Completed in 0.4011 seconds!
    [TL] container chef-server setup                             # Completed in 59.1569 seconds!
    [TL] container server-east-1 create                          # Completed in 7.3594 seconds!
    [TL] container server-east-1 up                              # Completed in 0.4014 seconds!
    [TL] container server-east-1 setup                           # Completed in 16.1263 seconds!
    [TL] container server-west-1 create                          # Completed in 8.0642 seconds!
    [TL] container server-west-1 up                              # Completed in 0.5014 seconds!
    [TL] container server-west-1 setup                           # Completed in 15.1147 seconds!

    $ tl status
    [TL] TestLab v0.5.4 Loaded

    NODES:
    +-----------+----------------------------------+---------+---------+----------------+------+----------------------------+-----+-----+
    | ID        | INSTANCE_ID                      | STATE   | USER    | IP             | PORT | PROVIDER                   | CON | NET |
    +-----------+----------------------------------+---------+---------+----------------+------+----------------------------+-----+-----+
    | localhost | testlab-repo-zpatten-zsp-desktop | running | vagrant | 192.168.33.239 | 22   | TestLab::Provider::Vagrant | 3   | 2   |
    +-----------+----------------------------------+---------+---------+----------------+------+----------------------------+-----+-----+

    NETWORKS:
    +-----------+------+---------+------------------+-----------+-------------+---------------+
    | NODE_ID   | ID   | STATE   | INTERFACE        | NETWORK   | NETMASK     | BROADCAST     |
    +-----------+------+---------+------------------+-----------+-------------+---------------+
    | localhost | east | running | br0:10.10.0.1/16 | 10.10.0.0 | 255.255.0.0 | 10.10.255.255 |
    | localhost | west | running | br1:10.11.0.1/16 | 10.11.0.0 | 255.255.0.0 | 10.11.255.255 |
    +-----------+------+---------+------------------+-----------+-------------+---------------+

    CONTAINERS:
    +-----------+---------------+-------+---------+--------+---------+--------------------------+---------------------------------------------------------------+
    | NODE_ID   | ID            | CLONE | STATE   | DISTRO | RELEASE | INTERFACES               | PROVISIONER                                                   |
    +-----------+---------------+-------+---------+--------+---------+--------------------------+---------------------------------------------------------------+
    | localhost | chef-server   | false | running | ubuntu | precise | west:eth0:10.11.0.200/16 | TestLab::Provisioner::AptCacherNG,TestLab::Provisioner::Shell |
    | localhost | server-east-1 | false | running | ubuntu | precise | east:eth0:10.10.0.254/16 | TestLab::Provisioner::AptCacherNG,TestLab::Provisioner::Shell |
    | localhost | server-west-1 | false | running | ubuntu | precise | west:eth0:10.11.0.254/16 | TestLab::Provisioner::AptCacherNG,TestLab::Provisioner::Shell |
    +-----------+---------------+-------+---------+--------+---------+--------------------------+---------------------------------------------------------------+
