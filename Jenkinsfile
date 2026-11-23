pipeline {
    agent any
    parameters {
        string(name: 'GREETING', defaultValue: 'Hello', description: 'The greeting message')
        choice(name: 'BRANCH', choices: ['master', 'feature/new-feature'], description: 'TimeRiddle branch to build')
        booleanParam(name: 'DEPLOY', defaultValue: false, description: 'Run the Deploy stage')
    }
    stages {
        stage('Checkout TimeRiddle') {
            steps {
                dir('TimeRiddle') {
                    git branch: "${params.BRANCH}", url: 'https://github.com/PeterPorzuczek/TimeRiddle.git'
                }
            }
        }
        stage('Example') {
            steps {
                echo "${params.GREETING}, we are building the ${params.BRANCH} branch."
                dir('TimeRiddle') {
                    bat 'dir'
                }
            }
        }
        stage('Deploy') {
            when {
                expression { params.DEPLOY }
            }
            steps {
                echo "Deploying ${params.BRANCH} branch..."
            }
        }
    }
}
