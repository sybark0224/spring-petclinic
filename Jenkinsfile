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
        git url: 'https://github.com/sybark0224/spring-petclinic.git', branch: 'main'  
      }
  
    }


        
  }
}        
        
