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
            echo 'build success'
        }
        failure {
            echo 'build failure'
        }
    }
}
