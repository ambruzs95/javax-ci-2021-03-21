pipeline {
    agent {
        docker { image 'adoptopenjdk:11-jdk-hotspot' }
    }
    stages {
        stage('Test') {
            steps {
                sh './gradlew test assemble'
            }
        }
		 stage('Integration Test') {
            steps {
                sh './gradlew integrationTest assemble'
            }
        }
    }
}