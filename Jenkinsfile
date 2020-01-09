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
//stage ('Deploy To Prod'){
  //input{
  //  message "Do you want to proceed for production deployment?"
 // }
   // steps {
              //  sh 'echo "Deploy into Prod"'
            //  }
      //  }
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
