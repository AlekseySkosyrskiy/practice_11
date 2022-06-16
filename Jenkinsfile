pipeline {
    agent any

    stages {
	stage('Deploy') {
		
            steps {
		    sh '''#!/bin/bash
		    	cd practice_11
			git pull
			docker run -d --name jenkins-practice -p 9889:80 --mount 'type=volume,src=app,dst=/usr/share/nginx/html' nginx
			'''
            }
        }
        stage('Check_http') {
            steps   {
		    script  {
			    final String url = "http://51.250.94.187:9889/"
		    final String response = sh(script: "curl -s -o /dev/null -w '%{http_code}' $url", returnStdout: true).trim()                    
			
			    if( response == "200" ) {
     				println "Got 200! All done!"
   			}else{
     				catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE')
			{
                    		echo "Not work!"
				notifyFailed()
                	}
   			}
		    }
	    }
        }
        
        stage('Check_md5') {
            steps {
		    script  {
		    final String md5 = sh(script: "md5sum '/home/sf-test/practice_11/index.html' | cut -d ' ' -f 1", returnStdout: true).trim()
                    final String url = "http://51.250.94.187:9889/"
                    final String response = sh(script: "curl -s $url | md5sum | cut -d ' ' -f 1", returnStdout: true).trim()
			if( md5 == response ) {
     				println "same"
   			}else{
     				catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE')
			{
                    		echo "MD5 amount did not match!"
				notifyFailed()
                	}
   			}
		    }
            }
        }
        stage('Remove') {
            steps {
		    sh '''#!/bin/bash
		    docker stop jenkins-practice
		    docker rm jenkins-practice
		    '''
		    notifySuccessful()
            }
        }
    }
}
def notifyStarted() {
  // send to Slack
  slackSend (color: '#FFFF00', message: "STARTED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})")
}
def notifySuccessful() {
  slackSend (color: '#00FF00', message: "SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})")
}
def notifyFailed() {
  slackSend (color: '#FF0000', message: "FAILED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})")
}
