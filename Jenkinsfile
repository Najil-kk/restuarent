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
                    git clone https://github.com/Najil-kk/My-details.git

                    ls -la
                    ls -la My-details
                '''

                stash name: 'webpage',
                      includes: 'My-details/**',
                      useDefaultExcludes: false
            }
        }

        stage('Deploy') {
            agent {
                label 'deploynode'
            }

            steps {
                deleteDir()

                unstash 'webpage'

                sh '''
                    sudo rm -rf /var/www/html/*

                    sudo cp -r My-details/. /var/www/html/

                    ls -la /var/www/html/
                '''
            }
        }
    }
}
