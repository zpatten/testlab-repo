[![Dependency Status](https://gemnasium.com/zpatten/testlab-repo.png)](https://gemnasium.com/zpatten/testlab-repo)

# TestLab Example

This is all very much WIP.

If you are going to play with this; I would suggest cloning the `TestLab` and `LXC` gems to `vendor/checkouts` and `export GEMDEV=1`.  Chasing the `master` branch is the way to go for now.

* https://github.com/zpatten/testlab
* https://github.com/zpatten/lxc

If you want to see what is going on during all of this; open another terminal, locate the testlab.log file and proceed to tail it.

    $ tl setup
    [TL] TestLab v0.6.1 Loaded
    [TL] node vagrant create                                     # Completed in 59.8709 seconds!
    [TL] node vagrant up                                         # Completed in 1.9135 seconds!
    [TL] node vagrant setup                                      # Completed in 86.4850 seconds!
    [TL] network labnet create                                   # Completed in 0.1005 seconds!
    [TL] network labnet up                                       # Completed in 0.1004 seconds!
    [TL] network labnet setup                                    # Completed in 0.2052 seconds!
    [TL] container chef-server create                            # Completed in 246.0947 seconds!
    [TL] container chef-server up                                # Completed in 0.5031 seconds!
    [TL] container chef-server setup                             # Completed in 27.1048 seconds!
    [TL] container server-lb-1 create                            # Completed in 8.2647 seconds!
    [TL] container server-lb-1 up                                # Completed in 0.5047 seconds!
    [TL] container server-lb-1 setup                             # Completed in 22.1674 seconds!
    [TL] container server-www-1 create                           # Completed in 8.4646 seconds!
    [TL] container server-www-1 up                               # Completed in 0.5039 seconds!
    [TL] container server-www-1 setup                            # Completed in 23.4809 seconds!
    [TL] container server-redis-1 create                         # Completed in 8.1606 seconds!
    [TL] container server-redis-1 up                             # Completed in 0.7053 seconds!
    [TL] container server-redis-1 setup                          # Completed in 22.8762 seconds!

    $ tl status
    [TL] TestLab v0.6.1 Loaded

    NODES:
    +---------+----------------------------------+---------+---------+----------------+------+----------------------------+-----+-----+
    | ID      | INSTANCE_ID                      | STATE   | USER    | IP             | PORT | PROVIDER                   | CON | NET |
    +---------+----------------------------------+---------+---------+----------------+------+----------------------------+-----+-----+
    | vagrant | testlab-repo-zpatten-zsp-desktop | running | vagrant | 192.168.33.239 | 22   | TestLab::Provider::Vagrant | 4   | 1   |
    +---------+----------------------------------+---------+---------+----------------+------+----------------------------+-----+-----+

    NETWORKS:
    +---------+--------+---------+------------------+-----------+-------------+---------------+
    | NODE_ID | ID     | STATE   | INTERFACE        | NETWORK   | NETMASK     | BROADCAST     |
    +---------+--------+---------+------------------+-----------+-------------+---------------+
    | vagrant | labnet | running | br0:10.10.0.1/16 | 10.10.0.0 | 255.255.0.0 | 10.10.255.255 |
    +---------+--------+---------+------------------+-----------+-------------+---------------+

    CONTAINERS:
    +----------------------------------------------+
    |       NODE_ID: vagrant                       |
    |            ID: chef-server                   |
    |         CLONE: false                         |
    |          FQDN: chef-server.default.zone      |
    |         STATE: running                       |
    |        DISTRO: ubuntu                        |
    |       RELEASE: precise                       |
    |    INTERFACES: labnet:eth0:10.10.0.254/16    |
    |  PROVISIONERS: Resolv/AptCacherNG/Apt/Shell  |
    +----------------------------------------------+
    |       NODE_ID: vagrant                       |
    |            ID: server-lb-1                   |
    |         CLONE: false                         |
    |          FQDN: server-lb-1.default.zone      |
    |         STATE: running                       |
    |        DISTRO: ubuntu                        |
    |       RELEASE: precise                       |
    |    INTERFACES: labnet:eth0:10.10.0.20/16     |
    |  PROVISIONERS: Resolv/AptCacherNG/Apt/Shell  |
    +----------------------------------------------+
    |       NODE_ID: vagrant                       |
    |            ID: server-www-1                  |
    |         CLONE: false                         |
    |          FQDN: server-www-1.default.zone     |
    |         STATE: running                       |
    |        DISTRO: ubuntu                        |
    |       RELEASE: precise                       |
    |    INTERFACES: labnet:eth0:10.10.0.21/16     |
    |  PROVISIONERS: Resolv/AptCacherNG/Apt/Shell  |
    +----------------------------------------------+
    |       NODE_ID: vagrant                       |
    |            ID: server-redis-1                |
    |         CLONE: false                         |
    |          FQDN: server-redis-1.default.zone   |
    |         STATE: running                       |
    |        DISTRO: ubuntu                        |
    |       RELEASE: precise                       |
    |    INTERFACES: labnet:eth0:10.10.0.22/16     |
    |  PROVISIONERS: Resolv/AptCacherNG/Apt/Shell  |
    +----------------------------------------------+
