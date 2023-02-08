pipeline {
    agent any
    environment{
      CREDENTIALS = 'AWS_SSH_KEY' }
    options{timestamps()}
    stages {
        stage('Image builder') {
         steps {
             sh 'docker build -t ghcr.io/cmg1911/hello-2048/hello-2048:v1 .'
             sh 'docker-compose build'
             sh 'docker-compose push'
                }
        }
    
        stage('Connection') {
         steps {withCredentials([sshUserPrivateKey(credentialsId: 'ssh-amazon', keyFileVariable: 'CREDENTIALS')]) {
                 sh ''' ssh -i $CREDENTIALS ec2-user@34.244.150.14
                 docker pull ghcr.io/cmg1911/hello-2048/hello-2048:v1''' 
                 sh 'docker run --rm -p 80:80 ghcr.io/cmg1911/hello-2048/hello-2048:v1'
              }
         }
        }    
     } 
}

