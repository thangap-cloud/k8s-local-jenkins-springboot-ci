#!/usr/bin/env groovy
node {
  stage("maven build") {
    sh "mvn clean install"
  }

  stage("docker build") {
    sh "docker build -t app:1.0"
  }
}
