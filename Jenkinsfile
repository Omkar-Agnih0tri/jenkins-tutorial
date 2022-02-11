pipeline {
  agent any
    stages {
      stage("Build Docker image"){
       steps{
         sh "docker build -t build:v1"
       }
      }
    }
}
