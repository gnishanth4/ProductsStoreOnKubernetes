

pipeline {
  agent any
  environment { 
      BUID_ID = '${env.BUILD_ID}'
      JOB_NAME = '${env.JOB_NAME}'
    }  
  stages {
    
    stage('Build Docker Image') {
        steps {
             sh '''
                 cd /var/lib/jenkins/workspace/ASP-Dot-Net-Pipeline-Docker/MvcApp
                 docker build --rm -f "Dockerfile" -t mvc-app:1.0 .   
                ''' 
         
        }
    } 
  
          
  }
 }    

