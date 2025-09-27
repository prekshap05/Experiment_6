pipeline {
    agent any
    environment {
        DEPLOY_DIR = 'C:\\inetpub\\wwwroot' // IIS folder on Windows
    }
    stages {
        stage('Checkout') {
            steps {
                echo 'Cloning project from GitHub...'
                git branch: 'main', url: 'https://github.com/YourUsername/Jenkins_Web_App.git'
            }
        }
        stage('Build') {
            steps {
                echo 'Build Step: Checking workspace files'
                bat 'dir'
            }
        }
        stage('Test') {
            steps {
                echo 'Validating HTML syntax using tidy (optional)'
                // Uncomment below if tidy is installed
                // bat 'tidy -qe index.html'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying files to IIS web root'
                bat "xcopy /Y index.html ${DEPLOY_DIR}\\"
                bat "xcopy /Y style.css ${DEPLOY_DIR}\\"
                bat "xcopy /Y script.js ${DEPLOY_DIR}\\"
            }
        }
        stage('Run HTTP Server (Optional)') {
            steps {
                echo 'Skipping HTTP server, use IIS to access the site'
            }
        }
    }
    post {
        success {
            echo 'Pipeline finished successfully! Visit: http://localhost/index.html'
        }
        failure {
            echo 'Pipeline failed! Check build logs.'
        }
    }
}
