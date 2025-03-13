pipeline {
    agent any

    environment {
        SONAR_TOKEN = credentials('SONAR_TOKEN') // Récupère le token de Jenkins Credentials
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Jacobkitams/Myhospital.git'
            }
        }

        stage('Build and Test') {
            steps {
                bat './gradlew build'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh "./gradlew sonarqube -Dsonar.login=${SONAR_TOKEN}"
                }
            }
        }
    }
}