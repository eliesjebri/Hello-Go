pipeline {
    agent {
        docker {
            image 'golang:alpine'
//            args '-u root'
        }
    }
    
    stages {
        stage('Build') {
            steps {
                sh 'pwd'
                sh 'mkdir /app'
                sh 'cp -r * /app'
                sh 'cd /app && go mod download && go build -o main'
            }
            post {
                success {
                    archiveArtifacts artifacts: 'main', fingerprint: true
                }
            }
        }
        
        stage('Test') {
            steps {
                sh 'cd /app && go test -v'
            }
        }
    }
}
