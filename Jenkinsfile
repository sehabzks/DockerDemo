pipeline {
    agent any
    tools {
        maven 'Maven'
    }
    stages {
        stage('Build Maven') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], userRemoteConfigs: [[url: 'https://github.com/sehabzks/DockerDemo']]])
                bat 'mvn clean install'
            }
        }
        stage('Build docker image') {
            steps {
                script {
                    sh 'docker build -t sehabzks/app .'
                }
            }
        }
        stage('Push image to Hub') {
            steps {
                script {
                    docker.image("demo12:${env.BUILD_NUMBER}").run("-d -p 8080:8080 --name demo-container")
                }
            }
        }
    }
}
