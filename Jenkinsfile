pipeline {
    agent any

    stages {
        stage('Check_http') {
            steps   {
		    script  {
		    a=http://51.250.94.187:9889/
		    curl -I $a | head -n 1 | cut -d$' ' -f2
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
