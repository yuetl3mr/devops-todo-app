pipeline {
  agent any 
  stages {
    //docker build
    stage('Build and test'){
	    steps {
    	    sh 'ls -la'
          sh 'docker build -t devops-todo-app:lastest'
	    }
    }
    // stage('Push Dockerhub'){
    //     steps{
    //         sh 'docker push yuetl/devops-todo-app'
    //     }
    // }
  }
}