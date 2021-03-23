pipeline {
    agent {
        docker { image 'adoptopenjdk:11-jdk-hotspot' }
    }
    stages {
        stage('Build') {
            steps {
                sh './gradlew test assemble'
            }
        }
		 stage('Integration Test') {
            steps {
                sh './gradlew integrationTest'
            }
        }
    }
}