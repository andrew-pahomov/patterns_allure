#!groovy
node {
    def build_ok = true
        stage("Prepare") {
            sh 'chmod +x gradlew'
            sh 'java -jar ./artifacts/app-card-delivery.jar'
        }
    try{
        stage('Run tests') {
            sh './gradlew test --info -Dselenide.headless=true'
        }
    } catch(e) {
        build_ok = false
        echo e.toString()
    }
    stage("Generate Reports") {
          allure ([
                includeProperties: false,
                jdk: '',
                properties: [],
                reportBuildPolicy: 'ALWAYS',
                results: [[path: 'build/allure-results']]
          ])
    }
    if(build_ok) {
        currentBuild.result = "SUCCESS"
    } else {
        currentBuild.result = "FAILURE"
    }
}