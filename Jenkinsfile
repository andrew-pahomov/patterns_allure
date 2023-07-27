#!groovy
pipeline {
    agent any
    stages {
        stage("Prepare") {
            steps {
                sh 'chmod +x gradlew'
                sh 'java -jar ./artifacts/app-card-delivery.jar &'
            }
        }
        stage("Run tests") {
            steps {
                sh './gradlew test --info -Dselenide.headless-true'
            }
        }
    }
}