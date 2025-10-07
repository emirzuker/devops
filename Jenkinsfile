pipeline {
    agent any

    environment {
        SONARQUBE_ENV = 'sq1'   // Nom de ton serveur SonarQube dans Jenkins
    }

    stages {
        stage('Pull from Git') {
            steps {
                git branch: 'main', url: 'https://github.com/emirzuker/devops.git'
            }
        }

        stage('Clean') {
            steps {
                sh '$M2_HOME/bin/mvn clean'
            }
        }

        stage('Compile') {
            steps {
                sh '$M2_HOME/bin/mvn compile'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv("${SONARQUBE_ENV}") {
                    sh '$M2_HOME/bin/mvn sonar:sonar'
                }
            }
        }

        stage('Package') {
            steps {
                sh '$M2_HOME/bin/mvn package'
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished'
        }
    }
}
