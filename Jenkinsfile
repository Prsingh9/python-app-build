pipeline {
    agent any

    stages {
        // Stage 1: Clone Repository from GitHub
        stage('Clone Repository') {
            steps {
                // Replace with your actual GitHub repo URL
                git url:'https://github.com/Prsingh9/python-app-build.git',branch:'main
            }
        }

        // Stage 2: Install Dependencies
        stage('Install Dependencies') {
            steps {
                // Install dependencies from the requirements.txt file
                sh 'pip install -r requirements.txt'
            }
        }

        // Stage 3: Run Tests using Pytest
        stage('Run Tests') {
            steps {
                // Run tests in the 'tests' directory
                sh 'pytest tests/'
            }
        }

        // Stage 4: Build Artifact (Python package)
        stage('Build Artifact') {
            steps {
                // Build the package using setup.py
                sh 'python setup.py sdist'
            }
        }

        // Stage 5: Archive Build Artifacts
        stage('Archive Artifact') {
            steps {
                // Archive the created package (e.g., .tar.gz)
                archiveArtifacts artifacts: 'dist/*.tar.gz', fingerprint: true
            }
        }
    }
}
