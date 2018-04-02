pipeline {
    agent any
    notifyStarted()

    stages {
        stage ('Compile Stage') {
            steps {
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
            }
        }
    }
        notifySuccessful()

}

def notifyStarted() {
   // send to email
   emailext ( 
       subject: "STARTED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'", 
       body: """<p>STARTED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
         <p>Check console output at "<a href="${env.BUILD_URL}">${env.JOB_NAME} [${env.BUILD_NUMBER}]</a>"</p>""",
       recipientProviders: [[$class: 'DevelopersRecipientProvider']]
     )
 }

 def notifySuccessful() {
   emailext (
       subject: "SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
       body: """<p>SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
         <p>Check console output at "<a href="${env.BUILD_URL}">${env.JOB_NAME} [${env.BUILD_NUMBER}]</a>"</p>""",
       recipientProviders: [[$class: 'DevelopersRecipientProvider']]
     )
 }

 def notifyFailed() {
   emailext (
       subject: "FAILED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
       body: """<p>FAILED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
         <p>Check console output at "<a href="${env.BUILD_URL}">${env.JOB_NAME} [${env.BUILD_NUMBER}]</a>"</p>""",
       recipientProviders: [[$class: 'DevelopersRecipientProvider']]
     )
 }
