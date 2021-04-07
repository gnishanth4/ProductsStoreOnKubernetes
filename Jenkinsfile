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
            dotnet sonarscanner begin /k:"Aspweb-App"  /d:sonar.login="ee5f103702e5d3eb33b0c4733e0d5f87a2ecb57a"
            dotnet build C:/Users/Administrator/Source/Repos/Blogifier/Blogifier.sln 
            dotnet sonarscanner end /d:sonar.login="ee5f103702e5d3eb33b0c4733e0d5f87a2ecb57a" 
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
        powershell("msbuild  C:/Users/Administrator/Source/Repos/Blogifier/Blogifier.sln /t:Publish /p:Configuration=Debug")        
      }
    }
      stage('Push Artifacts to Hub') {
          
          steps {
            echo "Airtifact on ${env.BUILD_ID}-${env.JOB_NAME}-ASP.zip"
            powershell('msbuild C:/Users/Administrator/Source/Repos/Blogifier/Blogifier.sln /p:DeployOnBuild=true /p:WebPublishMethod=Package /p:PackageAsSingleFile=true /p:PackageLocation="C:/ProgramFiles/NexusRepo/1.2-${BUILD_ID}-${JOB_NAME}-aspcore.zip"')
          }
      } 
     
     
  }
 }    
}
