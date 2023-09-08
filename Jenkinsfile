pipeline {
    agent {
        docker {
            image 'node:16-buster-slim'
            args '-p 3000:3000'
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') { 
            steps {
                sh './jenkins/scripts/test.sh' 
            }
        }
        stage('Manual Approval') {
            steps {
                input message: 'Lanjutkan ke tahap Deploy? (Klik "Proceed" untuk ke tahap Deploy)' 
            }
        }
        stage('Deploy') { 
            steps {
                sh './jenkins/scripts/deliver.sh' 
                // Menunggu selama 1 menit (60 detik)
                script {
                    sleep(time: 60, unit: 'SECONDS')
                }
                sh './jenkins/scripts/kill.sh' 
            }
        }
    }
}