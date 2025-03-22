pipeline {
    agent any

    tools {
        jdk 'jdk11'  // Reference the JDK you configured in Jenkins
    }

    environment {
        JAVA_HOME = "${tool 'jdk11'}"
        PATH = "${JAVA_HOME}/bin:${env.PATH}"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/mrtlenovo/ocp.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }
    }

    post {
        success {
            echo 'Build succeeded!'
        }
        failure {
            echo 'Build failed. Please check the logs.'
        }
    }
}
