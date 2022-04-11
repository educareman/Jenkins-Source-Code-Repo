pipeline {
    agent any
    
    environment {
        DOCKERHUB_CREDENTIALS=credentials('educaremann-dockerhub')
    }
    

    stages {
        stage('Cloning Educaremann github repo') {
            steps {
               git branch: 'main', url: 'https://github.com/educareman/jenkins.git'
            }
        }
        stage('Building my docker image') {
            steps {
                sh 'docker build -t educaremann/best-img1:latest .'
            }
        }
        stage('Testing my already built docker-image') {
            steps {
                sh 'docker version | docker images | docker history educaremann/best-img1:latest'
            }
        }
        stage('Run and port-forward my docker image on appache') {
            steps {
                sh 'docker run -d -p 7000:80 educaremann/best-img1 | docker ps'
            }
        }
        stage('Login to my Docker-hub repository') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('Pushing to my docker-hub repository') {
            steps {
                sh 'docker push educaremann/best-img1:latest'
            }
        }
    }
    post {
        always {
            sh 'docker logout'
        }
    }
}
