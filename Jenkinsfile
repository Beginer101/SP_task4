pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/Beginer101/SP_task4.git', credentialsId: 'access_for_jenkins'
            }
        }
        
        stage('Build') {
            steps {
                script {
                    try {
                        bat 'cd C:\\Users\\User\\source\\repos\\SP_task4\\SP_task4 && "D:\\VS\\MSBuild\\Current\\Bin\\MSBuild.exe" SP_task4.sln /p:Configuration=Debug /p:Platform=x64 /m'
                    } catch (Exception e) {
                        echo "Build error: ${e.message}"
                        currentBuild.result = 'FAILURE'
                        error("Pipeline stopped due to build failure.")
                    }
                }
            }
        }
        
        stage('Test') {
            steps {
                script {
                    try {
                        bat '"C:\\Users\\User\\source\\repos\\SP_task4\\SP_task4\\x64\\Debug\\SP_task4.exe"'
                    } catch (Exception e) {
                        echo "Test error: ${e.message}"
                        currentBuild.result = 'FAILURE'
                        error("Pipeline stopped due to test execution failure.")
                    }
                }
            }
        }
    }
    
    post {
        always {
            cleanWs()
        }
        
        failure {
            echo "Pipeline failed. Check logs to fix the issues."
        }
        
        success {
            echo "Pipeline completed successfully!"
        }
    }
}