pipeline {
    agent {
        label {
            label ('built-in')
            customWorkspace ('/mnt/project/practice2')
            }
        }
        stage ('Making new directories') {
            steps {
                    sh 'cd /mnt/project/practice2 && rm -rf * && mkdir 22Q3'
                }
            }
            stage ('Clear all the directories') {
                steps {
                    sh 'cd /mnt/project/practice2/22Q3 && rm -rf *'
                }
            }
            stage ('Pulling the rpeo 22Q3') {
            steps {
                sh 'cd /mnt/project/practice2/22Q3 && git init && git remote add origin https://github.com/utkarshpatil646/practice.git && git pull origin 22Q3'
            }
        }
        stage ('Cleaning the previous contaniner and adding new one') {
            steps {
                sh 'docker stop 22Q3'
                sh 'docker rm 22Q3'
            }
        }
        stage ('permissions to index.html') {
            steps {
                sh 'chmod -R 777 /mnt/project/practice2'
            }
        }
        stage ('Copying the index.html files in httpd servers') {
            steps {
                sh 'docker cp /mnt/project/practice2/22Q3/index.html 22Q3:/usr/local/apache2/htdocs/'
            }
        }
    }
