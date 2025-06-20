pipeline {
    agent any
    triggers { githubPush() }
    environment {
        IMAGE = "ci-demo:${env.BUILD_NUMBER}"
    }
    stages {
        stage('Checkout') {
            steps { checkout scm }
        }
        stage('Build') {
            steps { sh "docker build -t $IMAGE ." }
        }
        stage('Deploy') {
            steps {
                sh '''
                  docker rm -f ci-demo || true
                  docker run -d --name ci-demo -p 8081:80 $IMAGE
                '''
            }
        }
    }
}
