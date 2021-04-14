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
    
    stage('SSH Into k8s Server'){
      steps{
        def remote = [:]
        remote.name = 'K8S master'
        remote.host = '172.31.35.53'
        remote.user = 'ubuntu'
        remote.password = 'apple@2021'
        remote.allowAnyHosts = true
      }  
    }
  }
}
