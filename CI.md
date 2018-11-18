# Continuous Integration pipeline

Now create a new Pipeline job in jenkins.

In the pipeline, select `Pipeline script from SCM`. SCM should be `Git`.

The repository URL is: https://github.com/eybye/devops-workshop.git

The Script Path is `Sample/Jenkinsfile`.

The Jenkins file instructs the pipeline job to run the docker command:

```bash
$> docker build -t devops/aspnetmvc:latest Sample
```

which builds an image based on the `Dockerfile` located in folder `Sample`, see [Jenkinsfile](Sample/Jenkinsfile)

## Dockerfile

The Dockerfile uses a multi-stage build, see [Dockerfile](Sample/Dockerfile)
