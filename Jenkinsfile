pipeline {
    agent any
    environment {
        PATH = "/opt/maven/bin:$PATH"
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }
        
        stage('SonarQube Analysis') {
            environment {
                scannerHome = tool 'bharath-sonarqube-scanner'
            }
            steps {
                withSonarQubeEnv('Bharath-SonarQube-Server') {
                    sh "${scannerHome}/bin/sonar-scanner"
                }
            }
        }
        
        stage('Quality Gate') {
            steps {
                script {
                    timeout(time: 1, unit: 'hours') {  // Corrected 'Hours' -> 'hours'
                        def qg = waitForQualityGate()  // Fixed function name
                        if (qg.status != 'OK') {  // Ensure 'OK' is capitalized correctly
                            error "Pipeline aborted due to Quality Gate failure: ${qg.status}"
                        }
                    }
                }
            }
        }
    }
}
