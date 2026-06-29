pipeline {
    agent any
    environment{
        DOCKER_CRED = credentials('DockerHub')
    }
    stages {
        stage('fetch-code') {
            steps {
                git branch: 'main',  url: 'https://github.com/Harshthakur6957/jenkins-demo.git'
            }
        }
        stage('build-image'){
            steps{
                sh 'docker build -t cheaterkook/jenkins-app:${BUILD_NUMBER} .'
            }
        }
        stage('verfiy-build'){
            steps{
                sh 'echo $DOCKER_CRED_PSW | docker login -u $DOCKER_CRED_USR --password-stdin'
                sh 'docker push cheaterkook/jenkins-app:${BUILD_NUMBER}'
            }
        }
        stage('update-minikube'){
            steps{
                sh 'kubectl set image deployment/pd1 jenkins-app=cheaterkook/jenkins-app:${BUILD_NUMBER}'
            }
        }
    }
}
