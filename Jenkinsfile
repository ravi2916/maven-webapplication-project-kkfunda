pipeline{

    agent any

    tools{
        maven 'maven-3.9.16'
    }
    stages{
        stage('Git Checkout')
        {
            steps{
                git branch: 'master',
                url : 'https://github.com/ravi2916/maven-webapplication-project-kkfunda.git'
            }
        }
        stage('Compile')
        {
            steps{
                sh 'mvn compile'
            }
        }
         stage('Build')
        {
            steps{
                sh 'mvn clean package'
            }
        }
        stage('Sonar Qube'){
            steps{
                sh 'mvn sonar:sonar'
            }
        }
        stage("Artifatcory Backup Nexus"){
            steps{
                sh 'mvn deploy'
            }
        }
        stage('Deploy To Tomcat'){
            steps{
                sh """
    curl -u rr:Ravi@123 \
    --upload-file target/maven-web-application.war \
    "http://15.206.187.13:8080//manager/text/deploy?path=/maven-web-application&update=true"
    """
            }
        }
    }
}
