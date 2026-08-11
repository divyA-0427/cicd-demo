pipeline {
    agent any

    options {
        skipDefaultCheckout(true)
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                bat 'mvnw.cmd clean compile'
            }
        }

        stage('Test') {
            steps {
                bat 'mvnw.cmd test'
            }
        }
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    bat 'mvnw.cmd clean verify org.sonarsource.scanner.maven:sonar-maven-plugin:sonar -Dsonar.projectKey=cicd-demo1 -Dsonar.projectName=cicd-demo1'
                }
            }
        }

        stage('Jar') {
            steps {
                bat 'mvnw.cmd package -DskipTests'
            }
        }

         stage('Docker Image') {
             steps {
                  bat 'docker build -t securitydemo1:latest .'
             }
         }

    }
}