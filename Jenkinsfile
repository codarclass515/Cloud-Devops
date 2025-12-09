pipeline {
    agent any

    environment {
        NETLIFY_SITE_ID ="8ed15e86-1640-4c09-9fe9-a46e2eda4e7a"
        NETLIFY_AUTH_TOKEN = credentials('netlify-token')
        NODE_ENV       = "development"
        REGION         = "us-east-1"
        LOG_LEVEL      = "debug"
        API_BASE_URL   = "https://api.example.com"
        BUILD_ID       = "005"
        BUILD_ENV      = "CI"
        BUILD_SERVER   = "jenkins-main"
        JOB_TYPE       = "build"
        EXECUTOR_ID    = "5"
        BUILD_VERSION  = "v1.0.6"
    }

    tools {
        nodejs 'NodeJS 20.19.0'
    }

    stages {

        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/Tunesky34/learn-jenkins-app.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm run test'
            }
        }

        stage('Build App') {
            steps {
                sh 'npm run build'
            }
        }

stage('Deploy') {
    steps {
        echo 'Deploying to Netlify...'
        sh '''
            echo "Deploying to Netlify..."
            netlify deploy --prod --auth=$NETLIFY_AUTH_TOKEN --site="8ed15e86-1640-4c09-9fe9-a46e2eda4e7a"
        '''
    }
}

    }

    post {
        success {
            echo "Build complete: ${env.BUILD_ENV}, ${env.LOG_LEVEL}, ${env.BUILD_VERSION}, ${env.JOB_TYPE}"
        }
        failure {
            echo "Build failed: ${env.BUILD_ENV}, ${env.LOG_LEVEL}, ${env.JOB_TYPE}"
        }
    }
}