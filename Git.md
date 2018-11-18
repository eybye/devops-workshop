# Install a git server as a docker container

I have used an open source Git server project called Gogs (https://gogs.io/): 

## Pull image from Docker Hub

The command below will pull the latest gogs image from Dockerhub.

```bash
$> docker pull gogs/gogs
```

You can either let Gogs store its data on the host machine or inside the container.

### Let Gogs store data on host machine

Create local directory for the docker volume:

```bash
$> mkdir -p /var/gogs
```

Now you're ready to start the Gogs image:

```bash
$> docker run --name=gogs -p 10022:22 -p 10080:3000 -v /var/gogs:/data gogs/gogs
```

The command will start a container from the gogs images named gogs with host port 10022 and 10080 mapped to internal ports 22 and 3000. The host directory /var/gogs is mounted to an internal directory called /data.

If you decided not to store Gogs data on the host machine, omit the '-v /var/gogs:/data'.

You can restart the container with:

```bash
$> docker start gogs
```

---

## Setup Gogs

With a browser, navigate to: localhost:10080

To setup Gogs, select:

> Database type: SQLite3

> Application URL: http://localhost:10080/  *!Port mapped to host machine was 10080*

Admin account settings:

> Username: gituser

> Password: gituser

> Admin email: git@user.com

Now you ready to finish the installation. Your default user will be `gituser`.

## Create a git repository

Create a new git repository by pressing the `+` sign.

Name the repository `aspnet-test`.

Select `.gitignore` to `c sharp`.

> Remember to check the `Initialize this repo...`

## Cloning the repo to local drive

To clone the git repo, we use the `http` protocol and not the `ssh` cause git per default uses port 22.

```bash
$> git clone http://localhost:10080/gituser/aspnet-test.git
```

## Adding sample project to Gogs

Now get the sample project from Github and copy it into your local git folder.

Add the files to git and push the changes.

```bash
$> git commit -am "first commit"
$> git push
```