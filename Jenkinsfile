node ('node') {

notifyStarted()

    stage 'Checkout'
    checkout scm
    gitCommit = sh(returnStdout: true, script: 'git rev-parse HEAD').trim()
    shortCommit = gitCommit.take(6)

    stage 'Pack'
    sh "docker build -t innroad-docker.jfrog.io/devops-logging:${shortCommit} ."

    stage 'Publish'
    sh "docker push innroad-docker.jfrog.io/devops-logging:${shortCommit}"

notifySuccessful()

}

def notifyStarted() {
      slackSend (message: "STARTED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})")
}
def notifySuccessful() {
      slackSend (message: "SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})")
}
