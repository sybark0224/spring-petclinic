pipeline {
  agent any

  tools {
    jdk 'JDK17'
    maven 'M3'
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerCredential')
    AWS_CREDENTIALS = credentials('AWSCredential')
    //GIT_CREDENTIALS = credentials('gitCredential')
    REGION = 'ap-northest-2'
  }

  stages {
    stage('Git Clone') {
      steps {
        echo 'Git Clone'
        git url: 'https://github.com/sybark0224/spring-petclinic.git',
          branch: 'main'
      }
    }
    //Maven 빌드작업
    stage('MavenBuild') {
      steps {
        echo 'Maven Build'
        sh 'mvn -Dmaven.test.failure.ignore-true clean package'
      }
    }

    //Docker Image
    stage('Docker Image Build') {
      steps {
        echo 'Docker Image build'
        dir("${env.WORKSPACE}") {
          sh """  <sybark0224>/spring
          docker build -t ychpark/spring-petclinic:$BUILD_NUMBER .
          docker tag ychpark/spring-petclinic:$BUILD_NUMBER m7098/spring-petclinic:latest
          """
        }
      }
    }
          

  //DockerHub Login
  stage('Docker Login') {
    steps {
      sh """
      echo $DOCKERHUB_ CREDENTIAL_PSW | docker login -u $DOCKERHUB_CREDENTIAL_USR --password-sdin
      docker push sybark0224/spring-petclinic:latest
      """
    }
  }        
  //Docker Image 삭제
 stage('Remove Docker Image') {
   steps {
     sh """
     docker rmi ychpark/spring-petclinic:$BUILD_NUMBER
     docker rmi ychpark/spring-petclinic:latest
     """
    }
  }

  }
}
  
