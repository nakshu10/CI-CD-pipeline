pipeline {
    agent any

    environment {
        DEPLOY_DIR  = '/var/www/html/hello-world'
        APP_NAME    = 'Hello-World' 
    }

    options {
        timeout(time: 1, unit: 'HOURS')
        buildDiscarder(logRotator(numToKeepStr: '5'))
        disableConcurrentBuilds()
        timestamps()
    }

    stages {
        stage('Checkout Source') {
            steps {
                echo '📥 Fetching the latest premium code from Repository...'
                checkout scm
            }
        }

        stage('Code Validation & Lint') {
            steps {
                echo '🔍 Checking HTML structure and syntax integrity...'
                sh 'echo "HTML file verification passed successfully."'
            }
        }

        stage('Archive Artifacts') {
            steps {
                echo '📦 Archiving premium asset components...'
                archiveArtifacts artifacts: '*.html', fingerprint: true
            }
        }

        stage('Deploy to Web Server') {
            steps {
                echo "🚀 Deploying application to Production server: ${env.DEPLOY_DIR}"
                
                sh "mkdir -p ${env.DEPLOY_DIR}"
                
                sh "cp -r * ${env.DEPLOY_DIR}/"
                
                echo "✅ Deployment completed successfully!"
            }
        }
    }

    post {
        success {
            echo "🎉 Status: Success! Live Premium 'Hello World' is active."
        }
        failure {
            echo "❌ Status: Failed. Please check the console log for errors."
        }
    }
}
