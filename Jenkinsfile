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

        stage('Docker Build & Deploy') {
            steps {
                sh '''
                docker build -t municipal-backend ./backend-java

                docker stop municipal-backend || true
                docker rm municipal-backend || true

                docker run -d \
                --name municipal-backend \
                -p 8080:8080 \
                municipal-backend
                '''
            }
        }
    }

    post {

        success {
            emailext(
                subject: "MunicipalPortal Build SUCCESS",
                body: """
Build completed successfully.

Project: ${env.JOB_NAME}
Build Number: ${env.BUILD_NUMBER}

Docker Deployment Completed.

Check Jenkins:
${env.BUILD_URL}
""",
                to: "chintavindhyavahini@gmail.com,dommetisai997@gmail.com,nagasaikadali411@gmail.com,harshithanamala04@gmail.com,8919698419l@gmail.com,potlabrahmendra799@gmail.com"
            )
        }


        failure {
            emailext(
                subject: "MunicipalPortal Build FAILED",
                body: """
Build failed.

Project: ${env.JOB_NAME}
Build Number: ${env.BUILD_NUMBER}

Check Jenkins:
${env.BUILD_URL}
""",
                to: "chintavindhyavahini@gmail.com,dommetisai997@gmail.com,nagasaikadali411@gmail.com,harshithanamala04@gmail.com,8919698419l@gmail.com,potlabrahmendra799@gmail.com"
            )
        }
    }
}