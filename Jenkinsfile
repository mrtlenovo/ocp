pipeline {
    agent any  // Use any available Jenkins agent
    
    tools {
        maven 'maven-latest'  // Reference Maven from Jenkins Global Tool Configuration
        jdk 'jdk11'  // Assuming JDK11 is configured in Global Tool Configuration
    }

    environment {
        JAVA_HOME = "${tool 'jdk11'}"  // Set JAVA_HOME if needed
        PATH = "${JAVA_HOME}/bin:${env.PATH}"
    }

    stages {
        stage('Checkout') {
            steps {
                // Clone the repository
                git branch: 'main', url: 'https://github.com/mrtlenovo/ocp.git'
            }
        }

        stage('Build') {
            steps {
                // Run Maven clean install
                sh 'mvn clean install'
            }
        }

        stage('Test') {
            steps {
                // Run unit tests
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                // Package the Java project (e.g., create JAR or WAR)
                sh 'mvn package'
            }
        }

        stage('Archive Artifacts') {
            steps {
                // Archive the packaged JAR or WAR file for later use
                archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
            }
        }
    }

    post {
        success {
            echo 'Build completed successfully!'
        }
        failure {
            echo 'Build failed. Please check the logs.'
        }
    }
}
