pipeline {
    agent {
        // docker {
        //     image 'adoptopenjdk:11-jdk-hotspot'
        //     args '--network jenkins'
        // }
        dockerfile {
            filename 'Dockerfile.build'
            args '--network jenkins --volume gradle-data:/root/.gradle'
        }
    }
    stages {
        stage('Build') {
            steps {
                sh './gradlew -PbuildNumber=$BUILD_NUMBER test assemble'
            }
        }
        // stage('Integration Test') {
        //     steps {
        //         sh './gradlew integrationTest'
        //     }
        // }
        // stage('Integration test on MariaDB') {
        //             steps {
        //                 sh './gradlew -Pspring.datasource.url=jdbc:mariadb://employees-it-mariadb/employees -Pspring.datasource.username=employees -Pspring.datasource.password=employees integrationTest'
        //             }
        // }
        // stage('SonarQube') {
        //     steps {
        //         sh './gradlew -PbuildNumber=$BUILD_NUMBER sonarqube -Dsonar.userHome=/tmp/.sonar -Dsonar.host.url=http://employees-sonarqube:9000'
        //     }
        // }
        // stage('Docker image') {
        //     steps {
        //         // sh './gradlew -PbuildNumber=${BUILD_NUMBER} docker'
        //         // sh docker build -t employees
        //         script {
        //             def customImage = docker.build("employees:${env.BUILD_NUMBER}")
        //         }
        //     }
        // }
        stage('E2E test') {
            steps {
                script {
                    dir ('./integration-tests') {
                        sh 'docker-compose -f docker-compose.prod.yml up --abort-on-container-exit '
                    }
                }
            }
        }
    }
}