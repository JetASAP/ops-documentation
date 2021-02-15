Networking
==========

Currently, `ops` supports two networking modes; usermode and bridged. In this
document we will dive into the differences between these networking modes and
when it makes sense to select one over the other.

## Native Networking

Note that by default you should probably just use the native networking
provided by your cloud provider. These instructions only exist if you
wish to build your own private cloud.

## Usermode Network
Usermode is the default and simplest mode of networking. It utilizes the ready
available network connection and shares it with the ops instance.

It is worth noting that the simplicity of usermode does come at a performance
cost. Therefore, while usermode is a good option for demos, testing, and local
development; it may not be a good choice for production environments.

No action is required to configure usermode networking, it is used by
default.

## Bridged Network
Bridged networking connects a virtual machine to a network using the host
computer's Ethernet adapter. For more information about bridged networking,
see this [article](https://en.wikipedia.org/wiki/Bridging_%28networking%29).

In addition to that, KVM hardware acceleration can only be achieved while
utilizing this networking mode. Because of this, having an Ethernet connection
is required to setup this networking mode.

If you attempt to set it up without it, you may see your SSH session be
terminated or see an error like "no DHCP packet received within 10s".

To setup bridged networking, use the following command...

```sh
$ sudo ops net setup
```

To tear down a networking bridge, use the following command...

```sh
$ sudo ops net reset
```

#### Enabling bridge for an instance

Once you have setup a networking bridge, you need to specify in your `ops run`
and `ops pkg load` command to utilize that bridge. To do so, pass the flag `-b`.
