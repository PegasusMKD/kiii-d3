pipeline {
    agent any
    stages {
        def app
        stage('Clone repository') {
            steps {
                checkout scm
            }
        }
        stage('Build image') {
            steps {
                app = docker.build("PegasusMKD/kiii-d3")
            }
        }
        stage('Push image') {
            steps {
                docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                    app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
                    app.push("${env.BRANCH_NAME}-latest")
                }
            }
        }
    }
}
