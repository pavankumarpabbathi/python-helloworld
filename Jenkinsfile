pipeline {
  environment {
    registry = "pavankumarpabbathe12/helloworld-app"
    DOCKERHUB_CREDENTIALS = credentials('dockercred')
    dockerImage = ''
  }
  agent any
  stages {
    stage('Cloning our Git') {
      steps {
        git branch: 'main',
            url: 'https://github.com/pavankumarpabbathi/python-helloworld.git'  
      }
    }
    stage('Login to Docker Hub') {      	
       steps{                       	
         sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'                		
         echo 'Login Completed'      
       }           
    }
    stage('Building image') {
      steps {
        sh "docker build -t $registry:$BUILD_NUMBER ."
      }
    }
    stage('Push image to Dockerhub') {
      steps {
        sh "docker push $registry:$BUILD_NUMBER"
      }
    }
    stage('Cleaning up') {
      steps {
        sh "docker rmi $registry:$BUILD_NUMBER"
      }
    }
  }
}