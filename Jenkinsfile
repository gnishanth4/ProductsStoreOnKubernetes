

pipeline {
  agent any
  def app
  environment { 
      BUID_ID = '${env.BUILD_ID}'
      JOB_NAME = '${env.JOB_NAME}'
    }  
  stages {
    
    stage('Build Docker Image') {
        steps {
         app = docker.build("ProductsStoreOnKubernetes/MvcApp") 
        }
    } 
  
          
  }
 }    

