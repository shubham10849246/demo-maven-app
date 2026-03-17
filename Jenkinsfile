pipeline {
    agent any

    environment {
        SONAR_TOKEN = credentials('sonar-token') // optional if using credentials
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/<your-username>/devops-demo-app.git'
            }
        }

        stage('Build & Test') {
            steps {
                sh 'mvn clean verify'
            }
        }

        stage('Sonar Scan') {
            steps {
                sh '''
                mvn sonar:sonar \
                -Dsonar.projectKey=demo-app \
                -Dsonar.host.url=http://13.233.166.208:9000 \
                -Dsonar.login=squ_a28a9962230428489c0fd51d4d2bdee3f4d143a5
                '''
            }
        }
    }
}
