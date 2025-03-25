pipeline {
    agent any

    environment {
        JAVA_HOME = '/usr/lib/jvm/java-17-openjdk-amd64'
        SONAR_HOST_URL = 'http://10.20.44.72:9000'
        SONAR_PROJECT_KEY = 'Calculator'
        SONAR_TOKEN = 'sqp_d1ea1591ecb41c18e42efa5bdd372c37838acb49'
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
                mvn clean verify sonar:sonar \
                -Dsonar.projectKey=calculator_new \
                -Dsonar.projectName='calculator_new' \
                -Dsonar.host.url=http://10.20.44.72:9000 \
                -Dsonar.token=calculator_new
                '''
            }
        }
    }
}
