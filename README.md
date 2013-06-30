[![Dependency Status](https://gemnasium.com/zpatten/testlab-repo.png)](https://gemnasium.com/zpatten/testlab-repo)

# TestLab Example

This is all very much WIP.

If you are going to play with this; I would suggest cloning the `TestLab` and `LXC` gems to `vendor/checkouts` and `export GEMDEV=1`.  Chasing the `master` branch is the way to go for now.

* https://github.com/zpatten/testlab
* https://github.com/zpatten/lxc

If you want to see what is going on during all of this; open another terminal, locate the testlab.log file and proceed to tail it.

Example `Labfile.chef_rubygem`:

    $ tl build
    [TL] TestLab v0.6.16 Loaded
    [TL] node vagrant create                                     # Completed in 62.4842 seconds!
    [TL] node vagrant setup                                      # Completed in 92.5214 seconds!
    [TL] network labnet create                                   # Completed in 0.1040 seconds!
    [TL] network labnet up                                       # Completed in 0.1049 seconds!
    [TL] network labnet setup                                    # Completed in 0.3014 seconds!
    [TL] container chef-server create                            # Completed in 821.5866 seconds!
    [TL] container chef-server up                                # Completed in 2.0127 seconds!
    [TL] container chef-server setup                             # Completed in 1180.0937 seconds!
    [TL] container chef-client create                            # Completed in 11.1886 seconds!
    [TL] container chef-client up                                # Completed in 2.0137 seconds!
    [TL] container chef-client setup                             # Completed in 90.0322 seconds!

    $ tl status
    [TL] TestLab v0.6.17 Loaded

    NODES:
    +--------------------------------------------+
    |            ID: vagrant                     |
    |   INSTANCE_ID: chef-rubygem-zsp-desktop    |
    |         STATE: running                     |
    |          USER: vagrant                     |
    |            IP: 192.168.33.18               |
    |          PORT: 22                          |
    |      PROVIDER: TestLab::Provider::Vagrant  |
    |  PROVISIONERS: Raring,Bind                 |
    +--------------------------------------------+

    NETWORKS:
    +----------------------------------+
    |       NODE_ID: vagrant           |
    |            ID: labnet            |
    |         STATE: running           |
    |     INTERFACE: br0:10.10.0.1/16  |
    |       NETWORK: 10.10.0.0         |
    |       NETMASK: 255.255.0.0       |
    |     BROADCAST: 10.10.255.255     |
    |  PROVISIONERS: Route             |
    +----------------------------------+

    CONTAINERS:
    +------------------------------------------------------+
    |       NODE_ID: vagrant                               |
    |            ID: chef-server                           |
    |         CLONE: false                                 |
    |          FQDN: chef-server.default.zone              |
    |         STATE: running                               |
    |        DISTRO: ubuntu                                |
    |       RELEASE: precise                               |
    |    INTERFACES: labnet:eth0:10.10.0.254/16            |
    |  PROVISIONERS: Resolv,AptCacherNG,Apt,RubyGemServer  |
    +------------------------------------------------------+
    |       NODE_ID: vagrant                               |
    |            ID: chef-client                           |
    |         CLONE: false                                 |
    |          FQDN: chef-client.default.zone              |
    |         STATE: running                               |
    |        DISTRO: ubuntu                                |
    |       RELEASE: precise                               |
    |    INTERFACES: labnet:eth0:10.10.0.20/16             |
    |  PROVISIONERS: Resolv,AptCacherNG,Apt,RubyGemClient  |
    +------------------------------------------------------+

    $ tl help
    NAME
        tl - TestLab - A toolkit for building virtual computer labs

    SYNOPSIS
        tl [global options] command [command options] [arguments...]

    VERSION
        0.6.17

    GLOBAL OPTIONS
        -l, --labfile=path/to/file - Path to Labfile (default: /home/zpatten/Dropbox/code/personal/testlab-repo/Labfile)
        --version                  - Display the program version
        -v, --[no-]verbose         - Show verbose output
        -q, --[no-]quiet           - Quiet mode
        --help                     - Show this message

    COMMANDS
        help      - Shows a list of commands or help for one command
        container - Manage containers
        network   - Manage networks
        node      - Manage nodes
        create    - Create the test lab
        destroy   - Destroy the test lab
        up        - Online the test lab
        down      - Offline the test lab
        setup     - Setup the test lab infrastructure
        teardown  - Teardown the test lab infrastructure
        build     - Build the test lab infrastructure
        status    - Display information on the status of the test lab
