pipeline {
    agent any

    stages {
        stage('Check_http') {
            steps   {
		    script  {
		    final String response = sh(script: "curl -s -o /dev/null -w '%{http_code}' http://51.250.94.187:9889/' | cut -d ' ' -f 1", returnStdout: true).trim()                    
			def str2 = "200"
			    if( response == str2 ) {
     				println "Got 200! All done!"
   			}else{
     				catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE')
			{
                    		echo "Not work!"
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
                	}
   			}
		    }
            }
        }
        stage('Deploy') {
            steps {
		    echo '123'
            }
        }
    }
}
