pipeline {
    agent any   
    stages {
        stage ('Compile Stage') {   
            steps {
                mail to:"ruban.yuvaraj@gmail.com", subject: "STARTED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'", body: "STARTED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'"                   
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
        post {
        success {
            mail to:"ruban.yuvaraj@gmail.com", subject: "SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'", body: "SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'"
        }
        failure {
            mail to:"ruban.yuvaraj@gmail.com", subject: "FAILED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'", body: "FAILED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'"
        }
        unstable {
            mail to:"ruban.yuvaraj@gmail.com", subject:"UNSTABLE: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'", body: "UNSTABLE: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'"
        }     
        changed {
            mail to:"ruban.yuvaraj@gmail.com", subject:"CHANGED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'", body: "CHANGED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'"
        }
    }
}
