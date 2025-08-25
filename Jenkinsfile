pipeline {
    agent any

    tools {
        dotnet 'dotnet6'   // Jenkins-ийн Global Tool Config-д "dotnet6" гэж тохируулсан байх ёстой
    }

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

        stage('Run tests') {
            steps {
                script {
                    if (env.BRANCH_NAME == 'develop') {
                        sh 'dotnet test --filter "Category=Unit"'
                    } else if (env.BRANCH_NAME == 'staging') {
                        sh 'dotnet test --filter "Category=Integration"'
                    } else {
                        echo "No test filter applied for branch: ${env.BRANCH_NAME}"
                    }
                }
            }
        }
    }
}



