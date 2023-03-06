pipeline {
    agent {
        docker {
            image 'golang:alpine'
            args '-u root'
        }
    }
    
    stages {
        stage('Build') {
            steps {
                sh '''
                echo "################### Start Stage Build ###################" 
                pwd
                mkdir /app
                cp -r * /app
                cd /app && go mod init main && go mod download && go build -o /app/main && pwd && ls
                '''
            }
            post {
                success {
                    archiveArtifacts artifacts: '/app/main', fingerprint: true
                }
            }
        }
        
        stage('Test') {
            steps {
                sh 'echo "################### Start Stage Test ###################" '
                sh 'cd /app && go test -v'
            }
        }
    }
}
