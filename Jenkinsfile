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
                    git clone https://github.com/Najil-kk/restuarent.git

                    ls -la
                    ls -la restuarent
                '''

                stash name: 'webpage',
                      includes: 'restuarent/**',
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

                    sudo cp -r restuarent/. /var/www/html/

                    ls -la /var/www/html/
                '''
            }
        }
    }
}
