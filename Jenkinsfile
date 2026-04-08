pipeline {
    agent any

    stages {

        stage('Clone Code') {
            steps {
                git branch: "${env.BRANCH_NAME}",
                    url: 'https://github.com/yashjadhao123/jadhav-task-docker.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t myapp:$BRANCH_NAME .'
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                docker stop myapp-$BRANCH_NAME || true
                docker rm myapp-$BRANCH_NAME || true
                docker run -d -p 80:80 --name myapp-$BRANCH_NAME myapp:$BRANCH_NAME
                '''
            }
        }
    }
}
