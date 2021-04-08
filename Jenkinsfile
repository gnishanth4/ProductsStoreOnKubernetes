pipeline {
  environment {
    registry = "gnishanth444/productsonkubernetes"
    registryCredential = 'docker-creds'
    dockerImage = ''
  }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git 'https://github.com/gnishanth4/ProductsStoreOnKubernetes.git'
      }
    }
    stage('Building image') {
      steps{
        
        script {
          dir('mvcapp') {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
          }
        }
      }
    }

    stage('Deploy Image to Hub') {
      steps{
        script {
          withDockerRegistry([ credentialsId: registryCredential,url: ""] ) {
            
            sh 'docker push gnishanth444/productsonkubernetes":$BUILD_NUMBER"'
          }
        }
      }
    }
    stage('Remove Unused docker image') {
      steps{
        sh "docker rmi $registry:$BUILD_NUMBER"
      }
    }
    
    stage('Deploy to cluster'){
      steps{
        sshagent(['kubernetes']){
        script {          
          try {
               sh "ssh -o StrictHostkeyChecking=no ubuntu@15.206.183.99 kubectl apply -f kubernete-deployment.yml"
          } catch(error){
               sh "ssh -o StrictHostkeyChecking=no ubuntu@15.206.183.99 kubectl create -f kubernete-deployment.yml"
          }
        }
       }
      }  
    }
  }
}
