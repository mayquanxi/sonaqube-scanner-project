pipeline {
    agent any
    environment {
        scannerhome = tool 'sonarqubescanner'
    }
    stages {
        stage('Sonarscanner') {
            steps {
                withSonarQubeEnv('sonarqubeserver') {
                    sh "${scannerhome}/bin/sonar-scanner -X"
                }        
                timeout(time: 2, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
        stage('Build and Test Nodeapps') {
            steps {
                nodejs('node') {
                  echo 'Install dependencies'
                  sh 'npm install'
                  sh 'npm start & sleep 10'
                  echo "access webapps before continue"
                  echo "address: http://172.18.0.2:3000"
                  input message: "did you check webapps, if you did it click Process to continue or didn't click Abort"
                }
            }
        }
    }
}

//https://medium.com/@rosaniline/setup-sonarqube-with-jenkins-declarative-pipeline-75bccdc9075f  #intruction