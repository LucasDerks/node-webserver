
pipeline {
    agent any
    script{
        def app
    }
    
    stages {
        stage('Clone repository') {
            steps {
                checkout scm
            }
        }
        stage('Build docker image') {
            agent {
                docker {
                    image 'docker:latest'
                }
            }
            steps {
                app = docker.build("lucas5523/node-webserver")
            }
        }
        stage('Push image') {
            agent {
                docker {
                    image 'docker:latest'
                }
            }
            steps {
                docker.withRegistry('https://registry.hub.docker.com', 'docker-hub') {
                    app.push("${env.BUILD_NUMBER}")
                    app.push("latest")
                }
            }
        }
    }
}