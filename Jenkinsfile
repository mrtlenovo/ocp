pipeline {
    agent any

    tools {
        maven 'maven-latest'  // Matches the Maven Global Tool Configuration.
        jdk 'jdk11'           // Use the JDK configured in Jenkins.
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
                // Example deployment step
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
