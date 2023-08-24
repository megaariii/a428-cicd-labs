node {
    def dockerImage = 'node:16-buster-slim'

    properties([
        pipelineTriggers([
            pollSCM('*/2 * * * *')
        ])
    ])

    stage('Build') {
        checkout scm
        docker.image(dockerImage).inside('-p 3000:3000') {
            sh 'npm install'
        }
    }

    stage('Test') {
        checkout scm
        docker.image(dockerImage).inside('-p 3000:3000') {
            sh './jenkins/scripts/test.sh'
        }
    }

    stage('Deploy') {
        checkout scm
        docker.image(dockerImage).inside('-p 3000:3000') {
            sh './jenkins/scripts/deliver.sh'
            sleep(60)
            sh './jenkins/scripts/kill.sh'
        }
    }
}
