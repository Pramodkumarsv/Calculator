pipeline {
    agent any
    
    stages {
        stage('Setup Environment') {
            steps {
                sh 'sudo apt update'
                sh 'sudo apt install maven -y'
                sh 'sudo apt install openjdk-17-jdk -y'
                sh 'export JAVA_HOME=$JAVA_HOME'
            }
        }

        stage('Checkout Source Code') {
            steps {
                git url: 'https://github.com/Pramodkumarsv/Calculator.git', branch: 'master'
            }
        }

        stage('Build and Compile') {
            steps {
                sh 'mvn clean compile'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                sh '''
                mvn clean verify sonar:sonar \
                  -Dsonar.projectKey=new \
                  -Dsonar.projectName='new' \
                  -Dsonar.host.url=http://10.20.44.72:9000 \
                  -Dsonar.token=sqp_0145dc8eae8330192257e87c14b9568a04efd1e8
                '''
            }
        }
    }
}
