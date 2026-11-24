pipeline {
    agent none

    stages {

        stage('Build') {
            agent {
                label 'buildnode'
            }

            steps {
                deleteDir()

                echo 'Starting Build Stage'

                sh '''
                    git clone https://github.com/Najil-kk/restuarent.git

                    echo "Repository cloned successfully"

                    ls -la
                    ls -la restuarent
                '''

                stash name: 'webpage',
                      includes: 'restuarent/**',
                      useDefaultExcludes: false

                echo 'Build Stage Completed'
            }
        }

        stage('Deploy') {
            agent {
                label 'deploynode'
            }

            steps {
                deleteDir()

                unstash 'webpage'

                echo 'Starting Nginx Deployment'

                sh '''
                    sudo mkdir -p /var/www/html

                    sudo rm -rf /var/www/html/*

                    sudo cp -r restuarent/. /var/www/html/

                    sudo systemctl restart nginx

                    echo "Deployment Completed Successfully"

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
