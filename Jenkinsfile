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
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }
        stage('Deploy our image') {
            steps {
                script {
                    docker.withRegistry( registry, registryCredential ) {
                        dockerImage.push()
                    }
                }
            }
        }
        stage('Cleaning up') { 
            steps { 
                sh "docker rmi $registry:$BUILD_NUMBER" 
            }
        } 
    }
}