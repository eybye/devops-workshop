# Continuous Delivery pipeline

In the continuous delivery pipeline, we want to extend the CI pipeline by:

- Stopping and removing the current running container
- Starting the newly built image.

## Stopping and removing current container

By using the buldin Groovy script, we can `try` and remove a container, which might not exist.

Insert the following code as a new stage under the Docker build stage:

```
    stage('Stop existing container') {
      agent any
      steps {
        script {
          try {
            sh  '''
              docker rm -f aspnetmvc
            '''
          }
          catch (exc) {
              echo 'Container was not running'
          }
        }
      }
    }
```

## Starting the newly built image

To startup a new image, simply insert the following stage and last one:

```
    stage('Docker deploy') {
      agent any
      steps {
        sh 'docker run -d --name=aspnetmvc -p 8100:80 devops/aspnetmvc:latest'
      }
    }
```

The container is started in daemon mode and host port 8100 mapped to the internal port 80. Access the container using a webbrowser on url: localhost:8100
