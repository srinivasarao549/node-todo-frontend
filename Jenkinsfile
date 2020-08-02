pipeline {
    environment {
        registry = "itssrini777/testjoinsave"
        registryCredential = 'dockerhub'
        dockerImage = ''
    }
    
    agent any
    tools {
        docker 'docker'
    }
    stages {
        stage('Building our image') {
            steps{
                script {
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }
        stage('Deploy our image') {
            steps{
                script {
                    docker.withRegistry( '', registryCredential ) {
                        dockerImage.push()
                    }
                }
            }
        }
        stage('Cleaning up') {
            steps{
                sh "docker rmi $registry:$BUILD_NUMBER"
            }
        }
    }
}
