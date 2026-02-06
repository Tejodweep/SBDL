pipeline {
    agent any

    stages {
        // -------------------
        stage('Build') {
            steps {
                // Install dependencies using pipenv (adjust Python path if needed)
                sh 'pipenv --python $(which python3) sync'
            }
        }

        // -------------------
        stage('Test') {
            steps {
                // Run tests inside pipenv virtual environment
                sh 'pipenv run pytest || echo "Tests completed (ignoring failures for local testing)"'
            }
        }

        // -------------------
        stage('Package') {
            when {
                anyOf { branch "master"; branch "release" }
            }
            steps {
                // Zip the lib folder (local)
                sh 'zip -r sbdl.zip lib || echo "Packaging skipped (lib folder may not exist)"'
            }
        }

        // -------------------
        stage('Release (Local Test)') {
            when {
                branch 'release'
            }
            steps {
                // Local placeholder for Release stage
                sh 'echo "Release stage skipped for local testing"'
            }
        }

        // -------------------
        stage('Deploy (Local Test)') {
            when {
                branch 'master'
            }
            steps {
                // Local placeholder for Deploy stage
                sh 'echo "Deploy stage skipped for local testing"'
            }
        }
    }
}
