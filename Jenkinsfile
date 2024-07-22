pipeline {
    agent any
    stages {
        stage ('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/Natella-rex/Vulnerable-Web-Application.git'
            }
        }
        stage('Code Quality Check via SonarQube') {
            steps {
                script {
                    def scannerHome = tool 'SonarQube';
                    // Print the path of SonarQube scanner
                    sh "echo SonarQube Scanner Path: ${scannerHome}"

                    withSonarQubeEnv('SonarQube') {
                        sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=OWASP -Dsonar.sources=. -Dsonar.host.url=http://localhost:9000 -Dsonar.token=sqp_*********************************************"
                    }
                }
            }
        }
    }
    post {
        always {
            recordIssues enabledForFailure: true, tool: sonarQube()
        } 
    } 
} 
