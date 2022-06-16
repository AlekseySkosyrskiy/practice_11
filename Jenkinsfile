pipeline {
    agent any

    stages {
        stage('Check_http') {
            steps   {
		        script  {			    
                	int status = sh(script: "curl -sLI -w '%{http://51.250.94.187:9889/}' $url -o /dev/null", returnStdout: true)
			        if (status != 200 && status != 201) {
				        error("Returned status code = $status when calling $url") }                
		  	            }
	    	        }
        }
        
        stage('Check_md5') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
