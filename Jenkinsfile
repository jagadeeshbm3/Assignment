pipeline {
    agent any
    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', credentialsId: 'github', url: 'https://github.com/jagadeeshbm3/Assignment.git'
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
                sh 'docker tag jhooq-docker-demo jagadeeshbm/jhooq-docker-demo:jhooq-docker-demo'
            }
        }
        stage('dockerhub login') {
            steps {
                withCredentials([string(credentialsId: 'DOCKER_HUB_PASSWORD', variable: 'PASSWORD')]) {
                    sh 'docker login -u jagadeeshbm -p $PASSWORD'
                }
            }
        }
        stage('Push Image to Docker Hub') {
            steps {
                sh 'docker push  jagadeeshbm/jhooq-docker-demo:jhooq-docker-demo'
            }
        }
        stage('Deploy spring boot') {
            steps {
                script {
                    kubernetesDeploy(configs: "k8s-spring-boot-deployment.yml", kubeconfigId: "kubeconfig")
                }
            }
        }
    }
}



        
        
     
