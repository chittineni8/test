pipeline {
    environment {
        registry = "registry.codilar.in/codilar/test"
        registryCredential = 'docker-registry'
        dockerImage = ''
    }
    agent any
    stages {
        stage('Building our image') {
            steps {
                script {
                    dockerImage = docker.build registry + ":latest"
                }
            }
        }
        stage('Deploy our image') {
            steps {
                script {
                    docker.withRegistry( 'https://registry.codilar.in', registryCredential ) {
                        dockerImage.push()
                    }
                }
            }
        }
        stage('Cleaning up') { 
            steps { 
                sh "docker rmi $registry:latest" 
            }
        } 
    }
}