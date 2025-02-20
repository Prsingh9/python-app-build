pipeline {
    agent any

    stages {
        // Stage 1: Clone Repository from GitHub
        stage('Clone Repository') {
            steps {
                git url: 'https://github.com/Prsingh9/python-app-build.git', branch: 'main'
            }
        }

        // Stage 2: Install Dependencies
        stage('Install Dependencies') {
            steps {
                // Install dependencies from the requirements.txt file
                sh 'pip install -r requirements.txt'
                
                // Ensure setuptools is installed
                sh 'pip install setuptools'
            }
        }

        // Stage 3: Run Tests (optional)
        stage('Run Tests') {
            when {
                expression {
                    return fileExists('tests')
                }
            }
            steps {
                sh 'pytest tests/'
            }
        }

        // Stage 4: Build Artifact (Python package)
        stage('Build Artifact') {
            steps {
                sh 'python setup.py sdist'
            }
        }

        // Stage 5: Archive Build Artifacts
        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'dist/*.tar.gz', fingerprint: true
            }
        }
    }
}
