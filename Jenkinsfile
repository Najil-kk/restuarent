
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
                    echo "Starting Build Stage"

                    git clone https://github.com/Najil-kk/restuarent.git

                    echo "Repository cloned successfully"

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
                    echo "Starting Deployment"

                    sudo rm -rf /var/www/html/*

                    sudo cp -r restuarent/. /var/www/html/

                    echo "Deployment completed successfully"

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
