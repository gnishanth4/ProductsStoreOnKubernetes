

pipeline {
  agent any

  environment { 
      BUID_ID = '${env.BUILD_ID}'
      JOB_NAME = '${env.JOB_NAME}'
    }  
  stages {
    
    stage('Build Docker Image') {
        steps {
        docker.build("./ProductsStoreOnKubernetes/MvcApp") 
        }
    } 
  
          
  }
 }    

