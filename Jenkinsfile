
pipeline {
    agent any
    
    stages {
        stage('Clone repository') {
            steps {
                script {
                    checkout scm
                }
            }
        }
        stage('Build docker image') {
            agent {
                docker {
                    image 'docker:latest'
                }
            }
            steps {
                script {
                    app = docker.build("lucas5523/node-webserver")
                }
            }
        }
        stage('Push image') {
            agent {
                docker {
                    image 'docker:latest'
                }
            }
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'docker-hub') {
                        app.push("${env.BUILD_NUMBER}")
                        app.push("latest")
                    }
                }
            }
        }
    }
}
