node {
  stage("Clone the project") {
    git branch: 'main', url: 'https://github.com/thangap-cloud/k8s-local-jenkins-springboot-ci.git'
  }

  stage("Compilation") {
    sh "mvn clean install -DskipTests"
  }

   stage("docker Build") {
    sh "docker build -t app:v1 ."
  } 
}
