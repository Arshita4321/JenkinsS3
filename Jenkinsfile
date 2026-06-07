pipeline {
    agent any

    tools {
        maven 'Maven 3.9.14'
    }

    stages {

        stage('Build + Test + Coverage') {
            steps {
                bat 'mvn clean verify'
            }
        }

        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }

        stage('Publish Test Results') {
            steps {
                junit 'target/surefire-reports/*.xml'
            }
        }

        stage('Publish Coverage') {
            steps {
                jacoco execPattern: 'target/jacoco.exec',
                       classPattern: 'target/classes',
                       sourcePattern: 'src/main/java'
            }
        }
    }
}