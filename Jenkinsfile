pipeline {
    agent any

    stages {
        stage('Pull Code') {
            steps {
                git branch: 'main', url: 'https://github.com/NikhileshS89/ci-cd-pipeline.git'
            }
        }

        stage('Setup Python') {
            steps {
                echo 'Checking Python version'
                bat '"C:\\Users\\YOUR_USERNAME\\AppData\\Local\\Programs\\Python\\Python312\\python.exe" --version'
            }
        }

        stage('Run app.py') {
            steps {
                echo 'Running app.py'
                bat 'app.py'
            }
        }

        stage('Build') {
            steps {
                echo 'Building...'
            }
        }

        stage('Deploy to S3') {
            steps {
                withAWS(credentials: 'aws-jenkins-creds', region: 'ap-southeast-2') {
                    s3Upload(
                        bucket: 'ci-cd-artifacts-nik',
                        workingDir: '.',
                        includePathPattern: 'index.html'
                    )
                }
            }
        }
    }
}

