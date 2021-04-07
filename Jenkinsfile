

pipeline {
  agent any
  environment { 
      BUID_ID = '${env.BUILD_ID}'
      JOB_NAME = '${env.JOB_NAME}'
    }  
  stages {
    
    stage('Sonar Analysis') {
        steps {
            sh( ''' dotnet tool install --global dotnet-sonarscanner
            dotnet sonarscanner begin /k:"Aspweb-App"  /d:sonar.login="f92b60580fbcc1c571ccee6f23f0c7866b0a8e20"
            dotnet build /var/lib/jenkins/workspace/ASP-Dot-Net-Pipeline-Docker/ProductsStoreOnKubernetes.sln
            dotnet sonarscanner end /d:sonar.login="f92b60580fbcc1c571ccee6f23f0c7866b0a8e20" 
            ''')    
        }
    } 
  
          
  }
 }    

