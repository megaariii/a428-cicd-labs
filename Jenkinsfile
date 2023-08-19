node {
    def dockerImage = 'node:16-buster-slim'

    properties([
        pipelineTriggers([
            pollSCM('*/2 * * * *')
        ])
    ])

    stage('Build') {
        docker.image(dockerImage).inside('-p 3000:3000') {
            sh 'npm install'
        }
    }

    stage('Test') {
        docker.image(dockerImage).inside('-p 3000:3000') {
            sh './jenkins/scripts/test.sh'
        }
    }
}
