#!groovy

pipeline {
  agent none
  stages {
    stage('Docker Build') {
      agent any
      steps {
          sh 'docker build -t hasanertenli13/jenkins:latest .'
      }
    }
    stage('Docker Push') {
      agent any
      steps {
          sh 'docker login -u $DockerHubUser -p $DockerHubPassword'
          sh 'docker push hasanertenli13/jenkins:latest'
      }
    }
    stage('Docker Start') {
      agent any
      steps {
          sh 'sshpass -p 1 ssh -t -t -o StrictHostKeyChecking=no root@192.168.220.128 uptime'
          sh 'docker login -u $DockerHubUser -p $DockerHubPassword'
          sh 'docker pull hasanertenli13/jenkins:latest'
         // sh 'docker stop jenkins'
         // sh 'docker rm jenkins'
          sh 'docker run -d -p 3000:3000 --name jenkins hasanertenli13/jenkins:latest'
      }
    }
  }
}