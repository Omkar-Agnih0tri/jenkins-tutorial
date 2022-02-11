pipeline {
  agent any
    stages {
      stage("Build Docker image"){
        steps{
          sh "docker build -t user9595481/jenkins:${BUILD_ID} ."

        }
      }
      stage("Add build image to docker regsitry"){
        steps{
          withCredentials([string(credentialsId: 'DOCKER_HUB_PASSWORD', variable: 'password')]) {
            sh "docker login -u user9595481 -p ${password}" 
            sh "docker push user9595481/jenkins:${BUILD_ID}"
          }
        }
      }
      stage("K8s Deployment"){
          steps{
             sh "chmod +x myscript.sh"
             sh "sh myscript.sh ${BUILD_ID}"
 
             sshagent(['ubuntu']) {
                 sh "scp -o StrictHostKeyChecking=no  newdep.yaml ubuntu@65.2.35.6:/home/ubuntu"
                 script{
                   try{
                      sh "ssh ubuntu@65.0.178.67 kubectl create -f newdep.yaml"
                   }
                   catch(error){
                        sh "ssh ubuntu@65.0.178.67 kubectl apply -f newdep.yaml"
                   }
                
                 }
             }           
            
          }
      }
    }
}
