
pipeline {
    agent none

    stages {

        stage('Build') {
            agent {
                label 'buildnode'
            }

            steps {
                deleteDir()

                sh '''
                    echo "Starting Build"

                    git clone https://github.com/Najil-kk/restuarent.git

                    ls -la restuarent
                '''

                stash name: 'webpage',
                      includes: 'restuarent/**',
                      useDefaultExcludes: false
            }
        }

        stage('Deploy') {
            agent {
                label 'buildnode'
            }

            steps {
                deleteDir()

                unstash 'webpage'

                sh '''
                    echo "Starting Nginx Deployment"

                    sudo mkdir -p /var/www/html

                    sudo rm -rf /var/www/html/*

                    sudo cp -r restuarent/. /var/www/html/

                    sudo systemctl restart nginx

                    echo "Nginx Deployment Successful"

                    ls -la /var/www/html/
                '''
            }
        }
    }

    post {
        success {
            echo 'BUILD AND DEPLOYMENT SUCCESSFUL!'
        }

        failure {
            echo 'BUILD OR DEPLOYMENT FAILED!'
        }
    }
}
