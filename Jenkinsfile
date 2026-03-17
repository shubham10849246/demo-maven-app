p
ipeline {
    agent any

    environment {
        // You can use this if you want to reference the token globally
        SONAR_TOKEN = credentials('sonar-token')
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/shubham10849246/demo-maven-app.git'
            }
        }

        stage('Build & Test') {
            steps {
                sh 'mvn clean verify'
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
