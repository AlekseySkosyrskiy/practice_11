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
		    final String md5 = sh(script: "md5sum '/home/sf-test/practice_11/index.html' | cut -d ' ' -f 1", returnStdout: true).trim()
			    echo md5
                    final String url = "http://51.250.94.187:9889/"

                    final String response = sh(script: "curl -s $url | md5sum | cut -d ' ' -f 1", returnStdout: true).trim()

                    echo response
	if( md5 == response ) {
     println "same"
   }else{
     println "not same"
   }
		    }
            }
        }
        stage('Deploy') {
            steps {
		    sh '''#!/bin/bash
			a=sudo md5sum "/home/sf-test/practice_11/index.html" | cut -d ' ' -f 1
			b= sh "curl -s http://51.250.94.187:9889/ | md5sum | | cut -d ' ' -f 1"
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
