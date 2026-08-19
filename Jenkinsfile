pipeline {
    agent any
    tools {
            maven 'Maven'
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'master',
                   url: 'https://github.com/Willgunter/jenkins-test.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn -B clean package -DskipTests'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn -B test'
            }
            post {
                always {
                    junit 'target/surefile-reports/*.xml'
                }
            }
        }
        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }
}
