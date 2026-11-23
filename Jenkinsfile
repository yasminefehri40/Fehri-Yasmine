pipeline {
    agent any
    tools {
        jdk 'JAVA_HOME'
        maven 'M2_HOME'
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
                dir('backend') {
                    sh 'mvn compile'
                }
            }
        }
    }
}
