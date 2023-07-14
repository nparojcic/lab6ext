pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub')
    }
    stages {
        stage('Init'){
            steps {
                sh 'docker rm -f $(docker ps -aq) || true'
            }
        }
        stage('Build'){
            steps {
                sh 'chmod +x deploy.sh'
                sh './deploy.sh'
            }
        }
        stage('Push'){
            steps {
                sh "echo \$DOCKERHUB_CREDENTIALS_PSW | docker login -u \$DOCKERHUB_CREDENTIALS_USR --password-stdin"
                sh 'docker tag trio-task-mysql:5.7 npeero/mytriotasksql1:latest'
                sh 'docker tag trio-task-flask-app npeero/mytriotaskflask1:latest'
                sh 'docker push trio-task-mysql:5.7 npeero/mytriotasksql1:latest'
                sh 'docker push trio-task-flask-app npeero/mytriotaskflask1:latest'
            }
        }
    }
}