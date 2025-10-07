pipeline {
    agent any

    tools {
        maven 'Maven3'   // Nom du Maven défini dans Jenkins Global Tool Configuration
        jdk 'JDK17'      // Nom du JDK défini dans Jenkins
    }

    environment {
        SONARQUBE_ENV = 'sq1'   // Nom exact de ton serveur SonarQube dans Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/emirzuker/devops.git'
            }
        }

        stage('Clean & Build') {
            steps {
                sh 'mvn clean compile'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv("${SONARQUBE_ENV}") {
                    sh 'mvn sonar:sonar'
                }
            }
        }

        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished'
        }
    }
}
