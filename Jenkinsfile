pipeline {
    agent any
    tools {
        jdk 'JAVA_HOME'
        maven 'M2_HOME'
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build Maven') {
            steps {
                dir('backend') {
                    sh 'mvn compile'
                }
            }
        }
        stage('SonarQube Analysis') {
            steps {
                dir('backend') {
                    withCredentials([string(credentialsId: 'sonar-token', variable: 'SONAR_TOKEN')]) {
                        sh '''
                            mvn clean verify org.sonarsource.scanner.maven:sonar-maven-plugin:5.9.0.7382:sonar \
                              -Dsonar.projectKey=4SSA15_Fray \
                              -Dsonar.projectName=4SSA15_Fray \
                              -Dsonar.host.url=http://localhost:9000
                        '''
                    }
                }
            }
        }
    }
}
