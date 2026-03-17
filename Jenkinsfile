pipeline {
    agent any

    environment {
        // You can use this if you want to reference the token globally
        SONAR_TOKEN = credentials('sonar-token')
    }p

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/shubham10849246/demo-maven-app.git'
            }
        }

        stage('Build & Test') {
            steps {
                sh 'mvn clean package'
            }
        }

                stage('Docker Build') {
            steps {
                sh 'docker build -t demo-app .'
            }
        }

        stage('Push to Nexus') {
            steps {
                sh '''
                docker tag demo-app 13.233.166.208:8083/demo-app
                docker push 13.233.166.208:8083/demo-app
                '''
            }
        }

        stage('Push to JFrog') {
            steps {
                sh '''
                docker tag demo-app 13.233.166.208:8082/demo-app
                docker push 13.233.166.208:8082/demo-app
                '''
            }
        }

        stage('Sonar Scan') {
            steps {
                // Use credentials securely
                withCredentials([string(credentialsId: 'sonar-token', variable: 'SONAR_TOKEN')]) {
                    sh '''
                    mvn sonar:sonar \
                    -Dsonar.projectKey=demo-app \
                    -Dsonar.host.url=http://13.233.166.208:9000 \
                    -Dsonar.login=$SONAR_TOKEN
                    '''
                }
            }
        }
    }
}
