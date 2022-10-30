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
                sh "cd /mnt/project/ && sudo mvn clean install"
            }
       }
   }
}
