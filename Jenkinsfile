pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Restore dependencies') {
            steps {
                sh 'dotnet restore'
            }
        }
        stage('Build') {
            steps {
                sh 'dotnet build --no-restore'
            }
        }
        stage('Test') {
            steps {
                script {
                    if (env.BRANCH_NAME == "develop") {
                        sh 'dotnet test --filter "Category=Unit"'
                    } else if (env.BRANCH_NAME == "staging") {
                        sh 'dotnet test --filter "Category=Integration"'
                    }
                }
            }
        }
    }
}



