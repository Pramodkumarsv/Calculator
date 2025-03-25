pipeline {
    agent any

    environment {
        JAVA_HOME = '/usr/lib/jvm/java-17-openjdk-amd64'
        SONAR_HOST_URL = 'http://10.20.44.72:9000'
        SONAR_PROJECT_KEY = 'Calculator'
        SONAR_TOKEN = 'sqp_b1fdc78e7876193c3a3cc19446e35e9053c31eea'
    }

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
                mvn sonar:sonar \
                    -Dsonar.projectKey=${SONAR_PROJECT_KEY} \
                    -Dsonar.host.url=${SONAR_HOST_URL} \
                    -Dsonar.token=${SONAR_TOKEN}
                '''
            }
        }
    }
}
