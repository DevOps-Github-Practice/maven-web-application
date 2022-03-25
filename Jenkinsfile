node {
def mavenHome = tool name :"maven3.8.5"
stage('checkcode'){
git branch: 'development', credentialsId: '5bca85f3-160e-4747-9af0-22538bfece4a', url: 'https://github.com/DevOps-Github-Practice/maven-web-application.git'

}
stage('build'){
sh "$mavenHome/bin/mvn clean package"
}

stage('SonarQubeReport'){
sh "$mavenHome/bin/mvn sonar:sonar"
}

stage('UploadtoNexus'){
sh "$mavenHome/bin/mvn deploy"
}

stage('DeployApptoTomcat'){

sshagent(['5fce0f84-0826-4beb-82a9-161105e7734d']) {
    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@3.109.216.68:/opt/apache-tomcat-9.0.60/webapps"

}
}
}
