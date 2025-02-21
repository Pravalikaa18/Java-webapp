pipeline {
    agent any
    environment {
        // Set the correct path for the Git tool, if needed.
        GIT_TOOL = '/usr/bin/git' // Adjust this path if Git is installed elsewhere
        MAVEN_HOME = '/usr/share/maven' // Set Maven home if needed
    }
    stages {
        stage('Checkout SCM') {
            steps {
                script {
                    // Explicitly set Git installation path if needed
                    if (!fileExists(GIT_TOOL)) {
                        error("Git installation not found at $GIT_TOOL. Please install Git.")
                    }
                }
                checkout scm
            }
        }
        stage('List files in workspace') {
            steps {
                // List files in the workspace to confirm repository content and check if pom.xml exists
                sh 'ls -la'
            }
        }
        stage('Build') {
            steps {
                script {
                    // Check if pom.xml exists before running Maven
                    if (!fileExists('pom.xml')) {
                        error("Maven project descriptor (pom.xml) not found. Please check the repository.")
                    }
                }
                sh 'mvn clean package' // Build the project using Maven
            }
        }
        stage('Test') {
            steps {
                script {
                    if (!fileExists('pom.xml')) {
                        error("Maven project descriptor (pom.xml) not found. Skipping tests.")
                    }
                }
                sh 'mvn test' // Run Maven tests
            }
        }
        stage('Deploy to Tomcat') {
            steps {
                script {
                    if (!fileExists('target/*.war')) {
                        error("WAR file not found in target/ directory. Skipping deployment.")
                    }
                }
                sh 'scp target/*.war user@server:/var/lib/tomcat/webapps/' // Deploy to Tomcat
            }
        }
    }
    post {
        failure {
            echo 'Build failed. Please check the error messages above.'
        }
        success {
        
