pipeline {
    agent any
    environment {
        scannerhome = tool 'Sonarqubescanner'
    }
    stages {
        steps {
            withSonarQubeEnv('sonarqubeserver') {
                sh "${scannerhome}/bin/sonar-scanner"
            }        
            timeout(time: 2, unit: 'MINUTES') {
                waitForQualityGate abortPipeline: true
            }
        }
    }
}