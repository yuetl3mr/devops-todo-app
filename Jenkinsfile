pipeline {
  agent any 
  stages {
    stage('Hello'){
	    steps {
    	    echo 'Hello'
	    }
    }
    stage('List file'){
        steps{
            sh 'ls -la'
        }
    }
    stage('End'){
        steps{
            echo 'Finish'
        }
    }
  }
}