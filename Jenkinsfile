pipeline {
    agent any 
    environment {
        
        registry = "vetri19venki/department-service"
        registryCredential = 'docker_credential'
        dockerImage = ''
    }
    
    stages {
        stage('Cloning Git') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'f8b7d8fd-4a7c-4e71-a7ec-7a5f270b76a0', url: 'git@github.com:vetrivenki/department-service.git']]])
            }
        }
    
    
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry
        }
      }
    }
    
    stage('Upload Image') {
     steps{    
         script {
            docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
            }
        }
      }
    }
    
     stage('docker stop container') {
         steps {
            sh 'docker ps -f name=department-service -q | xargs --no-run-if-empty docker container stop'
            sh 'docker container ls -a -fname=department-service -q | xargs -r docker container rm'
         }
       }

    stage('Docker Run') {
     steps{
         script {
            dockerImage.run("-p 8080:8085 --rm --name department-service")
         }
      }
    }
  }
}
