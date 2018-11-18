# Git, Jenkins and Docker to build a CI/CD pipeline

This description is tested for linux/ubuntu only. It might work on other distros.

The prerequisite for following these descriptions is docker being installed on the host machine.

To get a nice web frontend for administering docker images and containers, install the [Portainer](https://hub.docker.com/r/portainer/portainer/) distro.

[Description on installing Jenkins](Jenkins.md)

To setup a CI (Continuous Integration) pipeline, follow the steps [here](CI.md).

To setup a CD (Continuous Delivery) pipeline, follow the steps [here](CD.md).

## Advanced

[Description on installing a local Github variant](Git.md)

---

## Using Gogs as Git repository

If you intend to use Gogs as repository, you need to create a network bridge to allow Gogs and Jenkins to communicate.

First create the bridge named `isolated_nw`:

```bash
$> docker network create --driver bridge isolated_nw
```

then both Gogs and Jenkins containers needs to be started with this additional parameter:

> --network=isolated_nw

this will attach the communication bridge and it is then possible to use the build-in service discovery. Using the container name in the host URL will automatically be resolved to an IP. E.g:
> http://gogs:3000/gituser/testrepo.git
