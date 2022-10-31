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
        stage ("Cloning the git repo") {
            steps {
                sh "sudo cd /mnt/project && sudo rm -rf *"
                sh "cd /mnt/project/ && git clone https://github.com/utkarshpatil646/practice.git"
            }
        }

        stage ("Installing the Application") {
            steps {
                sh "sudo chmod -R 777 /mnt"
                sh "sudo rm -rf /home/ansible/.m2/repository" 
                sh "cd /mnt/project/practice && mvn clean install"
            }
        }

        stage ("Copying the application from master to slave") {
            steps {
                sh "cd /mnt && ansible-playbook copy.yaml"
            }
        }

        stage ("Starting and deploying file on docker container") {
            agent {
                label {
                    label ('dev-a') 
                    customWorkspace ('/home/ansible/mnt')
                }
            }
            steps {
                sh "sudo systemctl start docker"
                sh "sudo docker stop utkarsh"
                sh "sudo docker rm utkarsh"
                sh "sudo chmod -R 777 /home/ansible/mnt"
                sh "sudo cd /home/ansible/mnt && sudo docker build -t utkarsh ."
                sh "sudo docker run -itdp 8080:8080 --name utkarsh utkarsh"
            }
        }
    }
}
