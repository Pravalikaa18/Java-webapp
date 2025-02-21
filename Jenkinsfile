pipeline {
    agent any
    environment {
        GIT_TOOL = '/usr/bin/git'  // Adjust this path if needed
        MAVEN_HOME = '/usr/share/maven'  // Adjust this path if needed
    }
    tools {
        // Declare Maven installation to ensure it is found
        maven 'Maven 3.x'  // Specify your Maven installation name
        git 'Default'       // Ensure Git tool is correctly set up
    }
    stages {
        stage('Checkout SCM') {
            steps {
                script {
                    // Check if Git is installed properly on Jenkins
                    if (!fileExists(GIT_TOOL)) {
                        error("Git installation not found at $GIT_TOOL. Please install Git.")
                    }
                }
                checkout scm
            }
        }
        stage('List files in workspace') {
            steps {
                // List files in the workspace to verify project structure
                sh 'ls -la'
            }
        }
        stage('Build') {
            steps {
                script {
                    // Check if pom.xml exists before building
                    if (!fileExists('pom.xml')) {
                        error("Maven project descriptor (pom.xml) not found. Please check the repository.")
                    }
                }
       
