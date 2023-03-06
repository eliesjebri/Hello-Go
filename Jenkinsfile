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
                cd /app && go mod init app && go mod download && go build -o /app/main 2>&1 | tee build.log
                //go build -o /app/main.bin && pwd && ls
                '''
            }
            post {
                always {
                    archiveArtifacts artifacts: '/app/main.bin', fingerprint: true
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
