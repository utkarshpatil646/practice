pipeline {
    agent {
        label {
            label ('built-in')
            customWorkspace ('/mnt/project/rutuja/')
            }
        }
        stages {}
        stage ('Making new directories') {
            steps {
                    sh 'cd /mnt/project/rutuja/ && rm -rf 22Q2 && mkdir 22Q2'
                }
            }
            stage ('Clear all the directories') {
                steps {
                    sh 'cd /mnt/project/rutuja/22Q2 && rm -rf *'
                }
            }
            stage ('Pulling the rpeo 22Q2') {
            steps {
                sh 'cd /mnt/project/rutuja/22Q2 && git init && git remote add origin https://github.com/utkarshpatil646/practice.git && git pull origin 22Q2'
            }
        }
        stage ('Cleaning the previous contaniner and adding new one') {
            steps {
                sh 'docker stop 22Q2'
                sh 'docker rm 22Q2'
            }
        }
        stage ('permissions to index.html') {
            steps {
                sh 'chmod -R 777 /mnt/project/rutuja'
            }
        }
        stage ('Copying the index.html files in httpd servers') {
            steps {
                sh 'docker cp /mnt/project/rutuja/22Q2/index.html 22Q2:/usr/local/apache2/htdocs/'
            }
        }
    }
}
