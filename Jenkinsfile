node
{
//"/var/lib/jenkins/tools/hudson.tasks.Maven_MavenInstallation/maven-3.9.16/bin"

def mvnHome=tool name : "maven-3.9.16"

stage('Git Checkout')
{
git credentialsId: '161b281b-5091-4745-9e23-894203f60737', url: 'https://github.com/ravi2916/maven-webapplication-project-kkfunda.git'
}
stage ('Compile')
{
 sh "${mvnHome}/bin/mvn compile"
}
stage ('Build')
{
sh "${mvnHome}/bin/mvn clean package"
}
stage ("Sonar")
{
sh "${mvnHome}/bin/mvn sonar:sonar"
}
stage ("Nexus")
{
sh "${mvnHome}/bin/mvn clean deploy"
}
stage('Deploy to Tomcat') {
    sh """
    curl -u rr:Ravi@123 \
    --upload-file target/maven-web-application.war \
    "http://13.127.52.74:8080/manager/text/deploy?path=/maven-web-application&update=true"
    """
}

}
