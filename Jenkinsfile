pipeline {
  agent none
  environment {
    PASSWORD = credentials('654321')  //refer secret documentation (https://www.way2automation.com/environment-variables-and-credentials-usage-in-jenkins-pipelines/)
  }
    stages {
      stage('create image') {
        agent {
		  label 'build'
		  }
		  steps {
                    sh 'docker build -t jmsaky/pipeimage .'
		    sh 'docker login -u jmsaky -p $PASSWORD'
		    sh 'docker push jmsaky/pipeimage'
          }           
         }
      stage('deploy container') {
	     agent {
		   label 'deploy'
		   }
		   steps {
                     sh 'docker login -u jmsaky -p $PASSWORD'
		     sh 'docker rm -f joseph'  
		     sh 'docker run -dit --name joseph -p 80:80 jmsaky/pipeimage'
		    
		   }              
          }
	 stage('App checking') {
	     agent {
		   label 'deploy'
		   }
		   steps {
                     sh 'curl http://localhost'
		   }              
          }   
         }
        }
