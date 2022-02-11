pipeline {
  agent any
    stages {
      stage("Build Docker image"){
        steps{
          sh "docker build -t jenkins/build:v1 ."

        }
      }
      stage("Add build image to docker regsitry"){
        steps{
          withCredentials([string(credentialsId: 'DOCKER_HUB_PASSWORD', variable: 'password')]) {
            sh "docker login -u user9595481 -p ${password}" 
            sh "docker push user9595481/jenkins:v1"
          }
        }
      }
    }
}
