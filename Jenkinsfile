pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                url: 'https://github.com/Techwing-Project-Week/MunicipalPortal.git'
            }
        }

        stage('Build Backend') {
            steps {
                dir('backend-java') {
                    sh 'mvn clean package -DskipTests'
                }
            }
        }
    }
}