pipeline {
  agent any

  tools {
    jdk 'jdk17'
    maven 'M3'
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerCredentials')
  }

  stages {
  //GitHub에서 
    stage('Git Clone') {
      steps {
        git url: 'https://github.com/sybark0224/spring-petclinic.git', branch: 'main'  
      }
  
    }
    stage('Maven Build') {
      steps {
        sh 'mvn -Dmaven.test.failure.ignore=true clean package'
      }
    }
    stage('Docker Image') {
      steps {
        dir("${env.WORKSPACE}") {
          sh """
          docker build -t ychpark/spring-petclinic:$BUILD_NUMBER .
          docker tag ychpark/spring-petclinic:$BUILD_NUMBER ychpark/spring-petclinic:latest
          """
        }
      }
    }
    stage('Docker Image Push') {
      steps {
        sh """
        echo $DOCKERHUB_CREDENTIALS_PSW |docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin
        docker push ychpark/spring-petclinic:latest
        """
      }
    }
    
  }
}        
        
