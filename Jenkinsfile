pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/KumaraswamyBakkashetti/login-app2.git'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                bat """
                echo Deploying to Tomcat...
                if not exist "C:\\apache-tomcat-9.0.112\\webapps\\loginapp" mkdir "C:\\apache-tomcat-9.0.112\\webapps\\loginapp"
                xcopy /Y /E "%WORKSPACE%\\*" "C:\\apache-tomcat-9.0.112\\webapps\\loginapp\\"
                echo Deployment Completed!
                """
            }
        }
    }

    post {
    success {
        emailext(
            subject: "SUCCESS: Login App Deployment #${env.BUILD_NUMBER}",
            body: """
            <h2 style='color:green;'>✔ Deployment Successful</h2>
            <p><b>Project:</b> ${env.JOB_NAME}</p>
            <p><a href='${env.BUILD_URL}'>View Build Details</a></p>
            """,
            mimeType: 'text/html; charset=UTF-8',
            to: "kumaraswamybakkashetti@gmail.com",
            replyTo: "",
            from: "kumaraswamybakkashetti@gmail.com",
            smtpHost: "smtp.gmail.com",
            smtpPort: "587",
            useTls: true
        )
    }
    failure {
        emailext(
            subject: "FAILED: Login App Deployment #${env.BUILD_NUMBER}",
            body: """
            <h2 style='color:red;'>❌ Deployment Failed</h2>
            <p><a href='${env.BUILD_URL}console'>Open Console Log</a></p>
            """,
            mimeType: 'text/html; charset=UTF-8',
            to: "kumaraswamybakkashetti@gmail.com",
            replyTo: "",
            from: "kumaraswamybakkashetti@gmail.com",
            smtpHost: "smtp.gmail.com",
            smtpPort: "587",
            useTls: true
        )
    }
}

}
