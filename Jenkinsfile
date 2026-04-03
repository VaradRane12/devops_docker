pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "izor12/devops-app"
    }

    stages {

        stage('Clone') {
            steps {
                git 'https://github.com/VaradRane12/devops_docker.git'
            }
        }

        stage('Build Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }

        stage('Login') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'USER',
                    passwordVariable: 'PASS'
                )]) {
                    sh 'echo $PASS | docker login -u $USER --password-stdin'
                }
            }
        }

        stage('Push') {
            steps {
                sh 'docker push $DOCKER_IMAGE'
            }
        }
    }
}
