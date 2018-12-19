pipeline {
    agent any
    stages {

        stage ('Initialize and Checkout') {
            steps {
                cleanWs()
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '', url: 'https://github.com/KamiKazi/cucumber-java-skeleton.git']]])
            }
        }

        stage('Automated Integration Tests') {
            steps {
                sh './gradlew test' //run a gradle task
            }
        }

        stage('Reporting') {
            steps {
                junit '**/build/test-results/test/*.xml'
                publishHTML (target: [
                        allowMissing: false,
                        alwaysLinkToLastBuild: false,
                        keepAll: true,
                        reportDir: 'build/reports/tests/test',
                        reportFiles: 'index.html',
                        reportName: "Cucumber Report"
                ])
            }
        }
    }
}