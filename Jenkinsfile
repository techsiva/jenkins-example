pipeline {
    agent any   

    stages {
        stage ('Compile Stage') {
            
            steps {
                notifyStarted()
                withMaven(maven : 'maven_3_5_0') {
                    sh 'mvn clean compile'
                }
            }
        }

        stage ('Testing Stage') {
            steps {
                withMaven(maven : 'maven_3_5_0') {
                    sh 'mvn test'
                }
            }
        }

        stage ('Deployment Stage') {
            steps {
                withMaven(maven : 'maven_3_5_0') {
                    sh 'mvn deploy'
                }
                notifySuccessful()
            }
        }
        stage('Send email') {
    def mailRecipients = "ruban.yuvaraj@gmail.com"
    def jobName = currentBuild.fullDisplayName

    emailext body: '''${SCRIPT, template="groovy-html.template"}''',
        mimeType: 'text/html',
        subject: "[Jenkins] ${jobName}",
        to: "${mailRecipients}",
        replyTo: "${mailRecipients}",
        recipientProviders: [[$class: 'CulpritsRecipientProvider']]
}
    }
        

}

def notifyStarted() {
   // send to email
   emailext ( 
       subject: "STARTED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'", 
       body: """<p>STARTED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
         <p>Check console output at "<a href="${env.BUILD_URL}">${env.JOB_NAME} [${env.BUILD_NUMBER}]</a>"</p>""",
       to: "${mailRecipients}",
       replyTo: "${mailRecipients}",
       recipientProviders: [[$class: 'DevelopersRecipientProvider']]
     )
 }

 def notifySuccessful() {
   emailext (
       subject: "SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
       body: """<p>SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
         <p>Check console output at "<a href="${env.BUILD_URL}">${env.JOB_NAME} [${env.BUILD_NUMBER}]</a>"</p>""",
       to: "${mailRecipients}",
       replyTo: "${mailRecipients}",
       recipientProviders: [[$class: 'DevelopersRecipientProvider']]
     )
 }

 def notifyFailed() {
   emailext (
       subject: "FAILED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
       body: """<p>FAILED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
         <p>Check console output at "<a href="${env.BUILD_URL}">${env.JOB_NAME} [${env.BUILD_NUMBER}]</a>"</p>""",
       to: "${mailRecipients}",
       replyTo: "${mailRecipients}",
       recipientProviders: [[$class: 'DevelopersRecipientProvider']]
     )
 }
