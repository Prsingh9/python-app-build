pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git url: 'https://github.com/Prsingh9/python-app-build.git', branch: 'main'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'python3 -m venv venv'
                sh './venv/bin/pip install -r requirements.txt'
                sh './venv/bin/pip install setuptools'
            }
        }

        stage('Run Tests') {
            when {
                expression {
                    return fileExists('tests')
                }
            }
            steps {
                sh './venv/bin/pytest tests/'
            }
        }

        stage('Build Artifact') {
            steps {
                sh './venv/bin/pip install setuptools'
                sh './venv/bin/python setup.py sdist'
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'dist/*.tar.gz', fingerprint: true
            }
        }
    }
}
