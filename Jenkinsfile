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
                cd /app && go mod init main && go mod download && CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -ldflags '-extldflags "-static"' -o main && pwd && ls
                '''
            }
            post {
                success {
                    archiveArtifacts artifacts: 'main', fingerprint: true
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
