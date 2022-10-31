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
        stage ("Cloning the Git Repo") {
            steps {
                sh "sudo rm -rf /.m2"
                sh "sudo rm -rf /mnt/project/*"
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
                sh "sudo ansible-playbook copy.yaml"
            }
       }
       stage ("Starting up docker on slave Dev-a") {
        agent {
            label {
            label ('dev-a')
            customWorkspace ('/mnt/')
            }
          }
             steps {
                sh "sudo systemctl start docker"
                sh "sudo cd /mnt/slave && sudo docker build -t Utkarsh"
                sh "sudo docker run -itd --name Utkarsh tomcat:9 bash"
            }
       }
   }
}
