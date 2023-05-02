node(){


        stage('Code Checkout'){
                checkout changelog: false, poll: false, scm: scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'GitHubCreds', url: 'https://github.com/dilawarkhan956/diladevops/']])
        }
        stage('Build Automation'){
                sh """
                        ls -lart
                        mvn clean install
                        ls -lart target
                """
        }


        stage('Code Deployment'){
                deploy adapters: [tomcat9(credentialsId: 'TomcatCreds', path: '', url: 'http://3.95.235.237:8080/')], contextPath: 'pipelinetestapp', onFailure: false, war: 'target/*.war'
        }

        stage('email notification'){
                mail bcc: '', body: """<p>SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>""", cc: 'dilwar.khan@hcl.com', from: '', replyTo: '', 
                subject: 'Test Application Notification', to: 'dilawarkhan956@gmail.com'

}
}
