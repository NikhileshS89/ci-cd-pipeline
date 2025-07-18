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
                echo 'Installing Python if required'
                // Make sure python is available, else install manually outside Jenkins
                sh 'python --version || echo "Python not found"'
            }
        }

        stage('Run app.py') {
            steps {
                echo 'Running app.py'
                sh 'python app.py'
            }
        }

        stage('Build') {
            steps {
                echo 'Building project...'
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

