node {
  checkout scm
  
  stage('Create Docker Image') {
    dir('ASP-Dot-Net-Pipeline-Docker') {
      docker.build("ASP-Dot-Net-Pipeline-Docker/MvcApp:${env.BUILD_NUMBER}")
    }
  }
  
} 
