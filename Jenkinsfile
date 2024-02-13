pipeline {
    agent any
    environment {
        SMPP_JAR_FILE="b2b-client"
    }

    stages {
        stage('Compile JAVA project') {
            steps {
                sh 'mvn clean install'
            }
        }
    }

    post {
        success {
            veracode canFailJob: true, scanPollingInterval: 30, scanName: "Jenkins - ${env.BUILD_NUMBER}", applicationName: "Java_HTS", criticality: "Medium", sandboxName: "VC-B2B-CLIENT", waitForScan: true, timeout: 30, deleteIncompleteScan: false, uploadIncludesPattern: "target/${env.SMPP_JAR_FILE}.jar", scanIncludesPattern: "target/${env.SMPP_JAR_FILE}.jar"
        }
    }
}
