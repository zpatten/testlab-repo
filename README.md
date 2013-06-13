[![Dependency Status](https://gemnasium.com/zpatten/testlab-repo.png)](https://gemnasium.com/zpatten/testlab-repo)

# TestLab Example

This is all very much WIP.

If you are going to play with this; I would suggest cloning the `TestLab` and `LXC` gems to `vendor/checkouts` and `export GEMDEV=1`.  Chasing the `master` branch is the way to go for now.

* https://github.com/zpatten/testlab
* https://github.com/zpatten/lxc

If you want to see what is going on during all of this; open another terminal, locate the testlab.log file and proceed to tail it.

    $ tl setup
    [TL] TestLab v0.6.1 Loaded
    [TL] node vagrant create                                     # Completed in 61.8821 seconds!
    [TL] node vagrant up                                         # Completed in 1.9162 seconds!
    [TL] node vagrant setup                                      # Completed in 109.5569 seconds!
    [TL] network labnet create                                   # Completed in 0.1008 seconds!
    [TL] network labnet up                                       # Completed in 0.1005 seconds!
    [TL] network labnet setup                                    # Completed in 0.1042 seconds!
    [TL] container chef-server create                            # Completed in 260.1049 seconds!
    [TL] container chef-server up                                # Completed in 0.4014 seconds!
    [TL] container chef-server setup                             # Completed in 26.4069 seconds!
    [TL] container server-lb-1 create                            # Completed in 8.1643 seconds!
    [TL] container server-lb-1 up                                # Completed in 0.4036 seconds!
    [TL] container server-lb-1 setup                             # Completed in 21.6694 seconds!
    [TL] container server-www-1 create                           # Completed in 8.1603 seconds!
    [TL] container server-www-1 up                               # Completed in 0.5035 seconds!
    [TL] container server-www-1 setup                            # Completed in 21.4627 seconds!
    [TL] container server-db-1 create                            # Completed in 8.1644 seconds!
    [TL] container server-db-1 up                                # Completed in 0.4047 seconds!
    [TL] container server-db-1 setup                             # Completed in 22.0673 seconds!
    [TL] container server-redis-1 create                         # Completed in 8.1644 seconds!
    [TL] container server-redis-1 up                             # Completed in 0.5044 seconds!
    [TL] container server-redis-1 setup                          # Completed in 22.6304 seconds!

    $ tl status
    [TL] TestLab v0.6.1 Loaded

    NODES:
    +---------+----------------------------------+---------+---------+----------------+------+----------------------------+-----+-----+
    | ID      | INSTANCE_ID                      | STATE   | USER    | IP             | PORT | PROVIDER                   | CON | NET |
    +---------+----------------------------------+---------+---------+----------------+------+----------------------------+-----+-----+
    | vagrant | testlab-repo-zpatten-zsp-desktop | running | vagrant | 192.168.33.239 | 22   | TestLab::Provider::Vagrant | 5   | 1   |
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
    |            ID: server-db-1                   |
    |         CLONE: false                         |
    |          FQDN: server-db-1.default.zone      |
    |         STATE: running                       |
    |        DISTRO: ubuntu                        |
    |       RELEASE: precise                       |
    |    INTERFACES: labnet:eth0:10.10.0.22/16     |
    |  PROVISIONERS: Resolv/AptCacherNG/Apt/Shell  |
    +----------------------------------------------+
    |       NODE_ID: vagrant                       |
    |            ID: server-redis-1                |
    |         CLONE: false                         |
    |          FQDN: server-redis-1.default.zone   |
    |         STATE: running                       |
    |        DISTRO: ubuntu                        |
    |       RELEASE: precise                       |
    |    INTERFACES: labnet:eth0:10.10.0.23/16     |
    |  PROVISIONERS: Resolv/AptCacherNG/Apt/Shell  |
    +----------------------------------------------+
