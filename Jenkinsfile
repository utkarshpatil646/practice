pipeline {
    agent {
        label {
            label ('built-in')
            customWorkspace ('/mnt/project/rutuja')
            }
        }
        stages {
            stage ('Making new directories') {
                steps {
                    sh 'cd /mnt/project/rutuja && rm -rf 22Q1 && mkdir 22Q1'
                }
            }
            stage ('Clear all the directories') {
                steps {
                    sh 'cd /mnt/project/rutuja/22Q1 && rm -rf *'
                }
            }
            stage ('Pulling the rpeo 22Q1') {
                steps {
                sh 'cd /mnt/project/rutuja/22Q1 && git init && git remote add origin https://github.com/utkarshpatil646/practice.git && git pull origin 22Q1'
            }
        }
            stage ('Cleaning the previous contaniner and adding new one') {
                steps {
                sh 'docker stop 22Q1'
                sh 'docker rm 22Q1'
            }
        }
            stage ('permissions to index.html') {
                steps {
                sh 'chmod -R 777 /mnt/project/rutuja'
            }
        }
            stage ('Copying the index.html files in httpd servers') {
                steps {
                sh 'docker cp /mnt/project/rutuja/22Q1/index.html 22Q1:/usr/local/apache2/htdocs/'
            }
        }
    }
}
