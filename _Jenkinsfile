node {
    def dockerImage

    try {
        dockerImage = docker.image('node:16-buster-slim').withRun('-p 3000:3000') {
            stage('Build') {
                sh 'npm install'
            }
            stage('Test') {
                sh './jenkins/scripts/test.sh'
            }
        }
    } finally {
        if (dockerImage != null) {
            dockerImage.stop()
        }
    }
}
