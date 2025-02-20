pipeline {
    agent any

    stages {
        // Stage 1: Clone Repository from GitHub
        stage('Clone Repository') {
            steps {
                git url: 'https://github.com/Prsingh9/python-app-build.git', branch: 'main'
            }
        }

        // Stage 2: Set up Virtual Environment
        stage('Set up Virtual Environment') {
            steps {
                // Create virtual environment
                sh 'python3 -m venv venv'
                
                // Activate virtual environment
                sh '. venv/bin/activate'
            }
        }

        // Stage 3: Install Dependencies
        stage('Install Dependencies') {
            steps {
                // Install dependencies inside the virtual environment
                sh 'venv/bin/pip install -r requirements.txt'
                sh 'pip install setuptools'
            }
        }

        // Stage 4: Run Tests using Pytest
        stage('Run Tests') {
            steps {
                // Run tests inside the virtual environment
                sh 'venv/bin/pytest tests/'
            }
        }

        // Stage 5: Build Artifact (Python package)
        stage('Build Artifact') {
            steps {
                // Build the package inside the virtual environment
                sh 'venv/bin/python setup.py sdist'
            }
        }

        // Stage 6: Archive Build Artifacts
        stage('Archive Artifact') {
            steps {
                // Archive the created package (e.g., .tar.gz)
                archiveArtifacts artifacts: 'dist/*.tar.gz', fingerprint: true
            }
        }
    }
}
