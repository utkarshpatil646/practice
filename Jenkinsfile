pipeline {
    agent {
        label {
          label ('built-in')
          customWorkspace ('/mnt/project/')   
        }
    }

    tools {
        maven "maven 3.8.6"
    }
    stages {
        stage ("Intializing git repo and Pulling the Repo") {
            steps {
                sh "sudo rm -rf cd /mnt/project/*"
                sh "cd /mnt/project/ && sudo git clone https://github.com/utkarshpatil646/practice.git"
            }
        }
       stage ("Installing the gameoflife.war"){
			steps {
                sh "sudo chmod -R 777 /mnt"
                sh "cd /mnt/project/practice && mvn clean install"
            }
       }
       stage ("copying the gameoflife.war in the dev envrinoment using SCP command") {
            steps {
                sh "sudo chmod -R 777 /mnt"
                sh "sudo cd /mnt/project/gameoflife-web/target/gameoflife.war /mnt"
                sh "sudo cd /mnt && sudo scp gameoflife.war ansible@20.10.1.254:/mnt"
            }
       }
    {
        label ('dev-a')
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
