pipeline {
agent any
stages {
stage('Source') {
steps {
checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/prabhavagrawal/discoveri-happytrip.git']]])
}
}
stage('Build') {
tools {
jdk 'jdk8'
maven 'apache-maven-3.6.1'
}
steps {
powershell 'java -version'
powershell 'mvn -version'
powershell 'mvn clean package'
archiveArtifacts 'target/*.war'
}
}
  stage('Approval') {
            steps {
                script {
                    def deploymentDelay = input id: 'Deploy', message: 'Deploy to production?', submitter: 'rkivisto,admin')]
                 //   sleep time: deploymentDelay.toInteger(), unit: 'HOURS'
                }
            }
        }
stage('Deploy') {
steps{
echo "Deploying"
deploy adapters: [tomcat7(credentialsId: 'tomcat', path: '', url: 'http://localhost:8085/')], contextPath: 'devops', onFailure: false, war: '**/*.war'
}
}
  
  stage('Email Notification'){
    steps{
    mail bcc: '', body: '''hi,

  Email Notification for Happytrip

Thanks,
Shobana A''', cc: '', from: '', replyTo: '', subject: 'Email Notification', to: 'testautomation991@gmail.com'
    
    }
  }
}
}
