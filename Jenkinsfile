pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/shubham10849246/demo-maven-app.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }
    }
}
