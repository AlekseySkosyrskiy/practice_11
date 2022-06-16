pipeline {
    agent any

    stages {
        stage('Check_http') {
            steps   {
		        script  {			    
                	int status = sh(script: '''curl -sLI -w '%{http://51.250.94.187:9889/}' $url -o /dev/null''', returnStdout: true)
			        if (status != 200 && status != 201) {
				        error("Returned status code = $status when calling $url") }                
		  	            }
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
