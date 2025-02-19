pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing...'
            }
        }
        stage('Vulnerability Scan') {
            steps {
                sh 'docker run --rm -v /var/run/docker.sock:/var/run/docker.sock aquasec/trivy:latest image web-app'
                }
	}
        stage('SonarQube analysis') {
            steps {
                withSonarQubeEnv(credentialsId: 'sqa_6c8cfdfd8b0331b359dd679c7d7d020c9bec44dc', installationName: 'SonarQubeScanner') {
                    sh 'sonar-scanner -Dsonar.projectKey=my_project -Dsonar.sources=/home/jenkins/my_project/src'
                }
            }
        }
    }
}
