# Docker

Use the docker slugs to refer to containers/images to avoid docker trying to resolve any ambiguities.
See example of docker pulling latest despite local image available. 

## Create New Docker Context

```bash
docker context create --docker host=tcp://10.10.10.10:2375 CONTEXT_LABEL
```

See other connection methods in the docks:

- [docker context docs](https://docs.docker.com/engine/reference/commandline/context_create/)


## List Docker Contexts

```bash
docker context ls
```

## Switch Docker Context

```bash
docker context use LABEL_OF_MY_CONTEXT
```

## Exec Interactive in Container

```bash
docker exec -it HASH_SLUG  sh
```

## List Containers

```bash
docker ps
```

## List images available

```bash
docker ps
```


