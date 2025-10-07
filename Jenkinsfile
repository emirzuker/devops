pipeline {
    agent any

    tools {
        jdk 'jdk17'              // Le JDK que tu as configuré dans Jenkins
        maven 'Maven-Local'      // Le Maven que tu as configuré dans Jenkins
    }

    stages {

        stage('Pull from Git') {
            steps {
                git branch: 'main', url: 'https://github.com/emirzuker/devops.git'
            }
        }

        stage('Clean') {
            steps {
                sh 'mvn clean'
            }
        }

        stage('Compile') {
            steps {
                sh 'mvn compile'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
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
        success {
            echo '✅ Build and analysis succeeded!'
        }
        failure {
            echo '❌ Build failed! Check logs.'
        }
    }
}
