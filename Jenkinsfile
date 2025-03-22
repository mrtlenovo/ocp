pipeline {
    agent any   // Runs the pipeline on any available Jenkins agent

    environment {
        MAVEN_HOME = '/usr/share/maven' // Path to Maven installation (adjust if different)
        JAVA_HOME = '/usr/lib/jvm/java-11-openjdk' // Path to Java installation
    }

    stages {
        stage('Checkout Code') {
            steps {
                // Checkout code from GitHub (assumes integration with GitHub)
                git branch: 'main', url: 'https://github.com/mrtlenovo/ocp.git'
            }
        }

        stage('Build') {
            steps {
                // Run Maven build
                sh '${MAVEN_HOME}/bin/mvn clean install'
            }
        }

        stage('Test') {
            steps {
                // Run unit tests using Maven
                sh '${MAVEN_HOME}/bin/mvn test'
            }
        }

        stage('Package') {
            steps {
                // Package the project (creates a .jar or .war)
                sh '${MAVEN_HOME}/bin/mvn package'
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
