pipeline {
  agent {
    kubernetes {
      yaml '''
        apiVersion: v1
        kind: Pod
        spec:
          containers:
          - name: maven
            image: maven:alpine
            command:
            - cat
            tty: true
          - name: docker
            image: docker:latest
            command:
            - cat
            tty: true
            volumeMounts:
             - mountPath: /var/run/docker.sock
               name: docker-sock
          volumes:
          - name: docker-sock
            hostPath:
              path: /var/run/docker.sock    
        '''
    }
  }
  stages {
    
    stage('Build-Jar-file') {
      steps {
        container('maven') {
          sh 'mvn package'
        }
      }
    }
    stage('Test-Docker-in Docker') {
      steps {
        container('docker') {
          sh 'sleep 600'
        }
      }
    }
    stage('Build-Docker-Image') {
      steps {
        container('docker') {
          sh 'docker build -t app:v1 .'
        }
      }
    }
    // stage('Login-Into-Docker') {
    //   steps {
    //     container('docker') {
    //       sh 'docker login -u <docker_username> -p <docker_password>'
    //   }
    // }
    // }
    //  stage('Push-Images-Docker-to-DockerHub') {
    //   steps {
    //     container('docker') {
    //       sh 'docker push ss69261/testing-image:latest'
    //   }
    // }
    //  }
  }
    // post {
    //   always {
    //     container('docker') {
    //       sh 'docker logout'
    //   }
    //   }
    // }
}