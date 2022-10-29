pipeline {
    agent {
        label ('built-in')
        customWorkspace('/mnt/project/')
    }

    tools {
        maven "maven 3.8.6"
    }
    stages {
        stage ("unziiping the ")
        stage ("Intializing git repo and Pulling the Repo") {
            steps {
                sh "cd /mnt/project/ && git init && git pull https://github.com/utkarshpatil646/practice.git"
            }
        }
        stage ("New agent"){
            agent {
            label ('dev')
        }
            steps {
                sh "sudo systemctl docker start"
                sh "cd /mnt/project/practice && mvn clean install"
            }
        }

        stage ("starting the docker container and deploying game of life in it") {
            steps {
                sh "docker run -itdp 8081:8080 -name utkarsh tomcat:9"
                sh "docker copy /mnt/project/practice/gameoflife-web/gameoflife.war utkarsh:/usr/local/tomcat/webapps"
            }
        }

    }
}
