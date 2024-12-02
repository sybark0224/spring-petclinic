pipeline {
  agent any

  tools {
    jdk 'jdk17'
    maven 'M3'
  }

stages {
  //GitHub에서 
  stage('Git Clone') {
    steps {
      git url: 'https://github.com/sybark0224/spring-petclinic/new/main.git', branch: 'main'  
    }
  
  }

 stage (Maven Build') {
    

  }
  stage ('Docker Image') {

  }
  stage ('Docker Image Push') {

  }
  stage ('SSH Publish') {

  }
        
  }
}        
        
