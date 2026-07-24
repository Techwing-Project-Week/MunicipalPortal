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

    post {
        success {
            emailext(
                subject: "MunicipalPortal Build SUCCESS",
                body: """
Build completed successfully.

Project: $PROJECT_NAME
Build Number: $BUILD_NUMBER

Check Jenkins:
$BUILD_URL
""",
                to: "chintavindhyavahini@gmail.com,dommetisai997@gmail.com,nagasaikadali411@gmail.com,harshithanamala04@gmail.com,8919698419l@gmail.com,potlabrahmendra799@gmail.com"
            )
        }

        failure {
            emailext(
                subject: "MunicipalPortal Build FAILED",
                body: """
Build failed.

Project: $PROJECT_NAME
Build Number: $BUILD_NUMBER

Check Jenkins:
$BUILD_URL
""",
                to: "chintavindhyavahini@gmail.com,dommetisai997@gmail.com,nagasaikadali411@gmail.com,harshithanamala04@gmail.com,8919698419l@gmail.com,potlabrahmendra799@gmail.com"
            )
        }
    }
}