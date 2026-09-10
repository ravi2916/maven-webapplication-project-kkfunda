pipeline
{
    agent any
    tools
    {
        maven 'maven-3.9.16'
    }
    stages {
        stage('Git Checkout')
        {
            steps{
                git branch : 'master',
                    url : 'https://github.com/ravi2916/maven-webapplication-project-kkfunda.git'
            }
        }
        stage('Compile & Build')
        {
            steps{
                parallel("Compile" : {
                    sh 'mvn compile'
                },"Build" : {
                    sh 'mvn clean package'
                }
                    )
            }
        }
        stage('SQ & Nexus')
        {
            steps{
                parallel("SQ":{
                    sh 'mvn sonar:sonar'
                },"Nexus":{
                    sh 'mvn deploy'
                }
                    )
            }
        }
        stage('Tomcat'){
            steps{
                 sh '''
                curl -u rr:Ravi@123 \
                --upload-file target/maven-web-application.war \
                "http://43.204.107.236:8080/manager/text/deploy?path=/maven-web-application&update=true"
                '''
            }
        }
    }
}












        
