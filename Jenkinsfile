pipeline {
    agent {
        label {
            label ('built-in')
            customWorkspace ('/mnt/project/practice2')
            }
        }
        stages {
            stage ('Making new directories') {
                steps {
                    sh 'cd /mnt/project/practice2 && rm -rf * && mkdir 22Q1 22Q2 22Q3'
                }
            }
            stage ('Clear all the directories') {
                steps {
                    sh 'cd /mnt/project/practice2/22Q1 && rm -rf *'
                    sh 'cd /mnt/project/practice2/22Q2 && rm -rf *'
                    sh 'cd /mnt/project/practice2/22Q3 && rm -rf *'
                }
            }
            stage ('Pulling the rpeo 22Q1') {
            steps {
                sh 'cd /mnt/project/practice2/22Q1 && git init && git remote add origin https://github.com/utkarshpatil646/practice.git && git pull origin 22Q1'
            }
        }
        stage ('Pulling the rpeo 22Q2') {
            steps {
                sh 'cd /mnt/project/practice2/22Q2 && git init && git remote add origin https://github.com/utkarshpatil646/practice.git && git pull origin 22Q2'
            }
        }
        stage ('Pulling the rpeo 22Q3') {
            steps {
                sh 'cd /mnt/project/practice2/22Q3 && git init && git remote add origin https://github.com/utkarshpatil646/practice.git && git pull origin 22Q3'
            }
        }
        stage ('permissions to index.html') {
            steps {
                sh 'chmod -R 777 /mnt/project/practice2'
            }
        }
        stage ('Installing Docker') {
            steps {
                sh 'yum install docker -y'
                sh 'systemctl start docker'
            }
        }
        stage ('Installing Httpd Server for 22Q1, 22Q2 and 22Q3 branches') {
            steps {
                sh 'docker pull httpd'
                sh 'docker run -itdp 81:80 --name 22Q1 httpd'
                sh 'docker run -itdp 82:80 --name 22Q2 httpd'
                sh 'docker run -itdp 83:80 --name 22Q3 httpd'
            }
        }
        stage ('Copying the index.html files in httpd servers') {
            steps {
                sh 'docker cp /mnt/project/practice2/22Q1/index.html 22Q1:/usr/local/apache2/htdocs/'
                sh 'docker cp /mnt/project/practice2/22Q2/index.html 22Q2:/usr/local/apache2/htdocs/'
                sh 'docker cp /mnt/project/practice2/22Q3/index.html 22Q3:/usr/local/apache2/htdocs/'
            }
        }
    }
}
