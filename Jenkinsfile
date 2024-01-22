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
            image: docker:19.03.1-dind
            securityContext:
              privileged: true
            env:
              - name: DOCKER_TLS_CERTDIR
                value: ""  
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
          sh 'sleep 10'
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