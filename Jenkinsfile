pipeline {
   agent any
   stages {
       stage('Clone Repository') {
           steps {
               git 'https://github.com/Java-webapp/java-webapp.git'
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
       stage('Deploy to Tomcat') {
           steps {
               sh 'scp target/*.war user@server:/var/lib/tomcat/webapps/'
           }
       }
   }
}
