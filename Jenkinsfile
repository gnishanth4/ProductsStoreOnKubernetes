String githubUrl = "https://github.com/gnishanth4/ProductsStoreOnKubernetes.git"

pipeline {
  agent any
  environment { 
      BUID_ID = '${env.BUILD_ID}'
      JOB_NAME = '${env.JOB_NAME}'
    }  
  stages {
    stage('Checkout') {
        steps {
        checkout([
            $class: 'GitSCM', 
            branches: [[name: 'master']], 
            doGenerateSubmoduleConfigurations: false, 
            extensions: [], 
            submoduleCfg: [], 
            userRemoteConfigs: [[url: """ "${githubUrl}" """]]])
     }        
    } 
    stage('Sonar Analysis') {
        steps {
            powershell( ''' dotnet tool install --global dotnet-sonarscanner
            dotnet sonarscanner begin /k:"Aspweb-App"  /d:sonar.login="f92b60580fbcc1c571ccee6f23f0c7866b0a8e20"
            dotnet build C:/Users/Administrator/Source/Repos/Blogifier/Blogifier.sln 
            dotnet sonarscanner end /d:sonar.login="f92b60580fbcc1c571ccee6f23f0c7866b0a8e20" 
            ''')    
        }
    } 
    stage('Clean') {
        steps {
            powershell('msbuild C:/Users/Administrator/Source/Repos/Blogifier/Blogifier.sln /t:Clean')
        }
    }
         
    stage('Build Code') {
      steps {
         
      }
    }
      stage('Push Artifacts to Hub') {
          
          steps {
          
          }
      } 
     
     
  }
 }    

