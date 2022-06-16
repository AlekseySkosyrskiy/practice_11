pipeline {
    agent any

    stages {
        stage('Check_http') {
            steps {
                //curl -I http://51.250.94.187:9889/ | head -n 1 | cut -d$' ' -f2
                while true
                    do
                        STATUS=$(curl -s -o /dev/null -w '%{http://51.250.94.187:9889/}')
                        if [ $STATUS -eq 200 ]; then
                            echo "Got 200! All done!"
                            break
                        else
                            echo "Got $STATUS :( Not done yet..."                                               
                    done

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
