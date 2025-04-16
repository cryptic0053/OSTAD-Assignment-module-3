pipeline {
    agent any

    tools {
        nodejs 'NodeJS 23' 
    }

    stages {
        stage('Clone') {
            steps {
                echo 'Cloning Repository...'
                git branch: 'main', url: 'https://github.com/cryptic0053/OSTAD-Assignment-module-3.git'
            }
        }

        stage('Install') {
            steps {
                echo 'Installing dependencies...'
                bat 'npm install'
            }
        }

        stage('Test') {
            steps {
                echo 'Running Tests...'
                script {
                    try {
                        bat 'npm run check'
                    } catch (err) {
                        currentBuild.result = 'FAILURE'
                        throw err
                    }
                }
            }
        }
    }

    post {
        always {
            echo "Build result: ${currentBuild.result}"
        }
        success {
            echo "✅ Build succeeded"
        }
        failure {
            echo "❌ Build failed"
        }
    }
}