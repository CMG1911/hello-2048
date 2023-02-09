pipeline {
    agent any
    options{timestamps()}
    stages {
        stage('Image builder') {
         steps {
            withCredentials([string(credentialsId: 'token-git', variable: 'CR_PAT')]) {
                sh "echo $CR_PAT | docker login ghcr.io -u CMG1911 --password-stdin"
                sh 'docker build -t ghcr.io/cmg1911/hello-2048/hello-2048:v1 .'
                sh 'docker-compose build'
                sh 'docker-compose push'}
            }
        }

        stage('Connection') {
         steps {sshagent(['ssh-amazon']) {
                 sh """
                    ssh -o "StrictHostKeyChecking no" ec2-user@ec2-54-195-160-88.eu-west-1.compute.amazonaws.com
                    """
                 sh 'docker pull ghcr.io/cmg1911/hello-2048/hello-2048:v1 '
                 sh 'docker run --rm -p 80:80 -d ghcr.io/cmg1911/hello-2048/hello-2048:v1' }
                }
       }
    }
}

