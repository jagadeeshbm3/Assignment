pipeline {
    agent any
    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', credentialsId: 'github_key', url: 'https://github.com/jagadeeshbm3/Assignment.git'
            }
        }
        stage('Gradle Build') {
            steps {
                sh './gradlew build'
            }
        }
        stage('Docker build') {
            steps {
                sh 'docker version'
                sh 'docker build -t jhooq-docker-demo .'
                sh 'docker image list'
                sh 'docker tag jhooq-docker-demo jagadeeshbm3/jhooq-docker-demo:jhooq-docker-demo'
            }
        }
        stage('dockerhub login') {
            steps {
                withCredentials([string(credentialsId: 'DOCKER_HUB_PASSWORD', variable: 'PASSWORD')]) {
                    sh 'docker login -u jagadeeshbm3 -p $PASSWORD'
                }
            }
        }
        stage('Push Image to Docker Hub') {
            steps {
                sh 'docker push  jagadeeshbm3/jhooq-docker-demo:jhooq-docker-demo'
            }
        }
    }
}





        
        
     
