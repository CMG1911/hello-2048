pipeline {
    agent any
     stages {
       stage('Builder') {
         steps {
             sh 'docker-compose build'
                }
        }
        stage('Deploy') {
            steps {
               sh 'docker-compose up -d'
            }
        }
     } 
}
