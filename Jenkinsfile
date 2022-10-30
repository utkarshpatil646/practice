pipeline {
    agent {
        label {
          label ('built-in')
          customWorkspace ('/mnt/project')   
        }
    }

    tools {
        maven "maven 3.8.6"
    }
    stages {
        stage ("Intializing git repo and Pulling the Repo") {
            steps {
                sh "cd /mnt/project/ && sudo git init && sudo git pull https://github.com/utkarshpatil646/practice.git"
            }
        }
       stage ("Installing the gameoflife.war"){
			steps {
                sh "cd /mnt/project/practice && sudo mvn clean install"
            }
       }
       stage ("copying the gameoflife.war in the dev envrinoment using SCP command") {
            steps {
                sh "sudo cd /mnt/project/gameoflife-web/target/gameoflife.war /mnt"
                sh "sudo cd /mnt && sudo scp gameoflife.war ansible@20.10.1.254:/mnt"
            }
       }
    {
        label ('dev')
        customWorkspace ('/mnt/')
    }
       stage ("Starting up docker") {
        steps {
            sh "sudo systemctl start docker"
            sh "sudo docker run -itdp 80:80 --name Utkarsh tomcat:9 bash"
            sh "sudo cd /mnt && sudo docker cp gameoflife.war Utkarsh:/usr/local/tomcat/webapps/"
        }
       }
   }
}
