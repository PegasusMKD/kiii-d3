node {
    def app
    stage('Clone repository') {
        checkout scm
    }
    stage ('Build image') {
        if(env.BRANCH_NAME == 'dev') {
            app = docker.build("pazzio/kiii-d3")    
        }
    }
    stage ('Push image') {
        if(env.BRANCH_NAME == 'dev') {
            docker.withRegistry('https://registry.hub.docker.com', 'docker-hub') {
                app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
                app.push("${env.BRANCH_NAME}-latest")
                //signal the orchestrator that there is a new version https://registry.hub.docker.com
            }
        }
    }
}
