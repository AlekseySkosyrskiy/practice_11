pipeline {
    agent any

    stages {
        stage('Check_http') {
            steps   {
		    sh '''#!/bin/bash

  STATUS=$(curl -s -o /dev/null -w '%{http_code}' http://51.250.94.187:9889/)
  if [ $STATUS -eq 200 ]; then
    echo "Got 200! All done!"
    break
  else
    echo "Got $STATUS :( Not done yet..."
    fi

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
		    sh '''#!/bin/bash
			a=md5sum "/home/sf-test/practice_11/index.html"
			b=curl -s "http://51.250.94.187:9889/" | md5sum
			if [$a == $b]
			then
			echo "All done!"
			else			
			catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE')
			{
                    		echo "MD5 amount did not match!"
                	}
			fi
		'''
            }
        }
    }
}
