pipeline {
    agent any

    tools {
        nodejs "Node16"   // Make sure this matches your Jenkins NodeJS tool name
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                echo "Installing packages..."
                sh 'npm install'
            }
        }

        stage('Run App') {
            steps {
                echo "Running application..."
                sh 'node index.js'
            }
        }

        stage('Archive Artifact') {
            steps {
                sh 'zip -r build_artifact.zip *'
                archiveArtifacts artifacts: 'build_artifact.zip', fingerprint: true
            }
        }
    }

    post {
        success {
            echo "✅ Build finished successfully!"
        }
        failure {
            echo "❌ Build failed — check console output."
        }
    }
}
