pipeline {
    agent any
    def app

    stages {
        stage('Clone repository') {
           checkout scm
        }
        stage('Build docker image') {
            app = docker.build("lucas5523/node-webserver")
        }
        stage('Push image') {
            docker.withRegistry('https://registry.hub.docker.com', 'docker-hub') {
                app.push("${env.BUILD_NUMBER}")
                app.push("latest")
            }
                echo "Pushing to DockerHub"

        }
    }
}