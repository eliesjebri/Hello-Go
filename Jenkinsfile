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
                cd /app && go mod init app && go mod download && ls -l && whoami && id -u && go build -v -o main 2>&1 | tee build.log
                '''
            }
            post {
                always {
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
