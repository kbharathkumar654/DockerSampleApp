pipeline {
    agent any
environment 
    {
    dockerhubcredential = credentials('dockerHub')
   }
 stages {
  stage('Docker Build and Tag') {
           steps {
                sh 'ls'
                sh 'docker build -t nginxtest:latest .'             
          }
        }
     
  stage('Publish image to Docker Hub') {
           steps {
             
               sh 'docker login -u $dockerhubcredential_usr -p $dockerhubcredential_psw'
              sh  'docker tag nginxtest nikhilnidhi/nginxtest:latest'
              sh  'docker push nikhilnidhi/nginxtest:latest'         
          }
        }
 stage('Run Docker container on remote hosts') {
             
            steps {
                sh "docker -H ssh://jenkins@172.31.28.25 run -d -p 4001:80 nginxtest"
 
            }
        }
    }
}