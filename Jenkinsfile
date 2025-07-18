pipeline {
    agent any

    stages {
        stage('Pull Code') {
            steps {
                git 'https://github.com/NikhileshS89/ci-cd-pipeline.git'
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
                        file: 'index.html',
                        path: 'index.html'
                    )
                }
            }
        }
    }
}

