pipeline {
    agent {
        docker {
            image 'node:22-alpine'
        }
    }

    environment {
        HOME = '.'
    }

    stages {
        stage('Environment') {
            steps {
                echo 'Checking the build environment inside the container'
                sh 'node --version'
                sh 'npm --version'
                sh 'id'
                sh 'head -2 /etc/os-release'
            }
        }
        stage('Install') {
            steps {
                echo 'Installing dependencies'
                sh 'npm install'
            }
        }
        stage('Build') {
            steps {
                echo 'Building the application'
                sh 'npm run build'
                sh 'ls -l dist'
            }
        }
    }

    post {
        success {
            archiveArtifacts artifacts: 'dist/**', fingerprint: true
            echo 'Build succeeded and artifacts were archived'
        }
        failure {
            echo 'Build failed. Read the console output above.'
        }
    }
}
