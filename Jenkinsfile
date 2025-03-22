pipeline {
    agent any

    tools {
        maven 'maven-latest'  // Change this to match your Maven Global Tool Configuration
        jdk 'jdk11'           // Make sure JDK11 is installed in Global Tool Configuration
    }

    environment {
        PROJECT_NAME = 'my-java-app'
        ARTIFACT_PATH = 'target/*.jar'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/mrtlenovo/ocp.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: "${ARTIFACT_PATH}", fingerprint: true
            }
        }

        stage('Deploy (Optional)') {
            when {
                expression { env.BRANCH_NAME == 'main' }
            }
            steps {
                echo "Deploying ${PROJECT_NAME} to production"
                // Example deployment step (this can vary based on your setup)
                // sh './deploy.sh'
            }
        }
    }

    post {
        success {
            echo 'Build and tests succeeded!'
        }
        failure {
            echo 'Build or tests failed. Check the logs.'
        }
    }
}
