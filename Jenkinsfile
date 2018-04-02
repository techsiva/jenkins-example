pipeline {
    agent any

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
            publishHTML (target: [ 
                allowMissing: false, 
                alwaysLinkToLastBuild: false, 
                keepAll: true, 
                reportDir: 'coverage', 
                reportFiles: 'index.html', 
                reportName: "RCov Report" 
            ]) 
            }
        }
    }
}
