pipeline {
    agent {
        label {
            label ('built-in')
            customWorkspace ('/mnt/project/utkarsh')
        }
    }
    tools {
        maven "maven 3.8.6"
    }
    stages {
        stage ('install-git, docker') {
            steps {
                sh 'yum install git docker  -y'
            }
        }
        stage ('cloning the git repository') {
            steps {
                sh 'cd /mnt/project/utkarsh && rm -rf * && git clone https://github.com/utkarshpatil646/practice.git'
            }
        }
        stage ('building the application') {
            steps {
                sh 'rm -rf /.m2/repository'
                sh 'cd /mnt/project/utkarsh/practice && mvn install'
            }
        }
        stage ('starting a container') {
            steps {
                sh 'systemctl start docker'
                sh 'docker run -itdp 8081:8080 --name Utkarsh tomcat:9'
            }
        }
        stage ('deploying gameoflife.war in container') {
            steps {
                sh 'docker cp /mnt/project/utkarsh/practice/gameoflife-web/target/gameoflife.war Utkarsh:/usr/local/tomcat/webapps/'
            }
        }
        stage ('Making new directories') {
            steps {
                sh 'cd /mnt/project && mkdir rutuja'
                sh 'cd /mnt/project/rutuja/ && rm -rf * && mkdir 22Q1 22Q2 22Q3'
                }
            }
        stage ('Clear all the directories') {
            steps {
                    sh 'cd /mnt/project/rutuja/22Q1 && rm -rf *'
                    sh 'cd /mnt/project/rutuja/22Q2 && rm -rf *'
                    sh 'cd /mnt/project/rutuja/22Q3 && rm -rf *'
                }
            }
        stage ('Cleaning the previous contaniner and adding new one') {
            steps {
                sh 'docker stop 22Q1 22Q2 22Q3'
                sh 'docker rm 22Q1 22Q2 22Q3'
                }
            }
        stage ('Pulling the rpeo 22Q1, 22Q2 & 22Q3') {
            steps {
                sh 'cd /mnt/project/rutuja/22Q1 && git init && git remote add origin https://github.com/utkarshpatil646/practice.git && git pull origin 22Q1'
                sh 'cd /mnt/project/rutuja/22Q2 && git init && git remote add origin https://github.com/utkarshpatil646/practice.git && git pull origin 22Q2'
                sh 'cd /mnt/project/rutuja/22Q3 && git init && git remote add origin https://github.com/utkarshpatil646/practice.git && git pull origin 22Q3'
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
                sh 'docker cp /mnt/project/rutuja/22Q2/index.html 22Q2:/usr/local/apache2/htdocs/'
                sh 'docker cp /mnt/project/rutuja/22Q3/index.html 22Q3:/usr/local/apache2/htdocs/'
            }
        }
    }
}
