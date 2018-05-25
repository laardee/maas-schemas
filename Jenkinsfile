node('ecs') {
    try {
        stage('Checkout repository') {
            checkout scm
        }
        withDockerContainer("node:8-alpine") {
            stage("Install") {
                sh """
                    npm install
                """
            }
            stage("Test") {
                sh """
                    npm run lint
                    npm test
                """
            }
        }
    } catch (e) {
        currentBuild.result = 'FAILURE'
        throw e
    } finally {
        cleanWs notFailBuild: true
    }
}
