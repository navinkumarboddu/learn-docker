# Communicate between multiple containers

Docker provides networking features to enable communication between containers, between containers and the host, and even between containers across different hosts. Here's an overview of Docker networking:
Basic Networking Commands:

## List Docker Networks:

  ```bash
   docker network ls
  ```

## Create a Docker Network:

```bash
docker network create <network-name>
```

Replace **<_network-name_>** with the desired name for your network.

## Inspect a Docker Network:

```bash
docker network inspect <network-name>
```

This provides detailed information about a specific network.


# Connecting Containers to a Network:

##    Start a Container and Connect to a Network:

  ```bash
docker run --network=<network-name> <image>
```

Replace **<_network-name_>** with the name of the network and **<_image_>** with the image you want to run.

## Default Networks:

### Bridge Network (Default):
        When you run a container without specifying a network, it's connected to the default bridge network.
        Containers on the same bridge network can communicate with each other.

###    Host Network:
        To have a container share the host network namespace, use the --network=host option.


## User-Defined Networks:

###    Create a User-Defined Network:

```bash
docker network create --driver bridge <network-name>
```

### Run Container on User-Defined Network:

```bash
docker run --network=<network-name> <image>
```

### Connect Existing Container to User-Defined Network:

```bash
docker network connect <network-name> <container-name>
```
