#!/usr/bin/env groovy
    agent any 
    stages {
        stage('Bulid App') {
            steps {
                sh "mvn clean install"
            }

        }
		// not in parallel due to race condition with .env
        stage('Docker Build') {
            steps {
                sh "docker build -t app:1.0 ."
            }
            
        }
        
    }
