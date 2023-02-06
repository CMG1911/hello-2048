pipeline {
    agent any
     stages {
        stage('SOM') {
            steps {
                git branch: 'main', url: 'https://github.com/CMG1911/hello-2048.git'
            }
        }
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
