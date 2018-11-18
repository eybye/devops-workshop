# Running Jenkins in a container

We'll use a special Jenkins distro which can utilize the hosts's Docker installation for building images and spinning up containers (https://github.com/liatrio/alpine-jenkins). To get this working, we need to mount the /var/run/docker.sock folder into the container.

Start jenkins:

```bash
$> docker run --name=jenkins -p 8080:8080 -v /var/run/docker.sock:/var/run/docker.sock liatrio/jenkins-alpine:lts
```

Username and password is: admin/admin
