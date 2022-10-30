pipeline {
    agent {
        label ('built-in')
        customWorkspace('/mnt/project/')
    }

    tools {
        maven "maven 3.8.6"
    }
    stages {
        stage ("Intializing git repo and Pulling the Repo") {
            steps {
                sh "cd /mnt/project/ && git init && git pull https://github.com/utkarshpatil646/practice.git"
            }
        }
       stage('delete customworkspace-QA-1'){
	             agent {
                    label ('20.20.1.254')
                    }
			steps {
                sh "sudo systemctl start docker"
                sh "cd /mnt/project/practice && sudo mvn clean install"
            }
        }

        stage ("starting the docker container and deploying game of life in it") {
            steps {
                sh "sudo docker run -itdp 8081:8080 -name utkarsh tomcat:9"
                sh "sudo docker cp /mnt/project/practice/gameoflife-web/gameoflife.war utkarsh:/usr/local/tomcat/webapps"
            }
        }
    }
}
