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
                withSonarQubeEnv(credentialsId: 'sqa_873515ff0915f3b6daa77f893fde4d0f27e0387f', installationName: 'SonarQubeScanner') {
                    sh 'sonar-scanner -Dsonar.projectKey=my_project -Dsonar.sources=/home/jenkins/my_project/src'
                }
            }
        }
    }
}
