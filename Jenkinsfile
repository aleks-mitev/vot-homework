pipeline {
    agent any
    triggers { githubPush() }
    environment {
        IMAGE = "ci-demo:${env.BUILD_NUMBER}"
    }
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/aleks-mitev/vot-homework.git', branch: 'main'
            }
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
