pipeline {
    agent any

    environment{
        Node_env = 'Development'
    }
    tools{
        nodejs 'NodeJS 20.19.0'
    }
    stages{
        stage ('clone repository'){
            steps{
            git branch: 'main', url: 'https://github.com/Tunesky34/Jenkins-image.git'
            }
        }
        stage('install dependencies'){
            steps{
                sh 'npm install'
            }
    }
        stage('run test'){
            steps{
                sh 'npm run test'
            }
        }
        stage('build test'){
            steps{
                sh 'npm run build'
            }
        }
    }
    post{
        success {
            echo 'successful'
        }
        failure {
            echo 'failed'
        }
    }   
}