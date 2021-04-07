

pipeline {
  agent any
  environment { 
      BUID_ID = '${env.BUILD_ID}'
      JOB_NAME = '${env.JOB_NAME}'
    }  
  stages {
    
    stage('Sonar Analysis') {
        steps {
            sh '''           
               dotnet tool install --global dotnet-sonarscanner
               dotnet sonarscanner begin /k:"aspwebapp" /d:sonar.host.url="http://65.1.149.144:9000"  /d:sonar.login="c2be390856ba4843f83dac7360b02100b1466e6b"
               dotnet build /var/lib/jenkins/workspace/ASP-Dot-Net-Pipeline-Docker/ProductsStoreOnKubernetes.sln
               dotnet sonarscanner end /d:sonar.login="c2be390856ba4843f83dac7360b02100b1466e6b" 
               
            '''   
        }
    } 
  
          
  }
 }    

