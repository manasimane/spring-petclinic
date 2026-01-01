pipeline {
    agent any

    tools {
        jdk 'jdk17'
    }

    stages {

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Build with Maven') {
            steps {
                sh './mvnw clean package -DskipTests'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t spring-petclinic:1.0 .'
            }
        }
    }
}
