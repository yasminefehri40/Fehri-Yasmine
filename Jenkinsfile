pipeline {
    agent any
    tools {
        jdk 'JAVA_HOME'
        maven 'M2_HOME'
    }
    environment {
        IMAGE = "yasminefehri/fehri-yasmine"
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/yasminefehri40/Fehri-Yasmine.git',
                    credentialsId: 'github-credentials'
            }
        }
        stage('Build Maven') {
            steps {
                dir('backend') { sh 'mvn compile' }
            }
        }
        stage('Package') {
            steps {
                dir('backend') { sh 'mvn package -DskipTests' }
            }
        }
        stage('Docker Build') {
            steps {
                dir('backend') { sh "docker build -t ${IMAGE}:latest ." }
            }
        }
        stage('Docker Push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials',
                                                  usernameVariable: 'DOCKER_USER',
                                                  passwordVariable: 'DOCKER_PASS')]) {
                    sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                    sh "docker push ${IMAGE}:latest"
                }
            }
        }
    }
}
