pipeline {
    agent any

    stages {
        stage('Check_http') {
            steps   {
		    sh '''#!/bin/bash

while true
do
  STATUS=$(curl -s -o /dev/null -w '%{http_code}' http://51.250.94.187:9889/)
  if [ $STATUS -eq 200 ]; then
    echo "Got 200! All done!"
    break
  else
    echo "Got $STATUS :( Not done yet..."
done
	   '''
	    }
        }
        
        stage('Check_md5') {
            steps {
		    script  {
                final String url = "http://51.250.94.187:9889/"

                    final String response = sh(script: "curl -s $url", returnStdout: true).trim()

                    echo response
		    }
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
