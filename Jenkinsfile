pipeline {
    agent any

    tools {
        jdk 'jdk17'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build App') {
            steps {
                sh './mvnw clean package -DskipTests'
            }
        }

        stage('Build & Push Docker Image') {
    steps {
        script {
            docker.withRegistry('https://index.docker.io/v1/', 'dockerhub-creds') {
                def app = docker.build("manasi880/spring-petclinic:${BUILD_NUMBER}")
                app.push()
                app.push("latest")
            }
        }
    }
}
        stage('Deploy Application') {
    steps {
        script {
            sh '''
              docker stop petclinic || true
              docker rm petclinic || true
              docker pull manasi880/spring-petclinic:ci
              docker run -d --name petclinic -p 8080:8080 manasi880/spring-petclinic:ci
            '''
        }
    }
}


    }
}
