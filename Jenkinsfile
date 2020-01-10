pipeline {
agent any
stages {
stage('Source') {
steps {
checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/prabhavagrawal/discoveri-happytrip.git']]])
}
}
 stage('SonarQube Analysis') {
        sonarqube 'sonar_scanner', 'http://localhost:9000'
    }
  }
 stage('Build) {
tools {
jdk 'jdk8'
maven 'apache-maven-3.6.1'
// sonarQube 'sonar_scanner'
}
steps {
powershell 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.2:sonar'
powershell 'java -version'
powershell 'mvn -version'
powershell 'mvn clean package'
archiveArtifacts 'target/*.war'
}
  }
  stage('Approval') {
            steps {
                script {
                    def deploymentDelay = input id: 'Deploy', message: 'Deploy to production?', submitter: 'shobana,admin'
                 
                }
            }
        }
  //With Delay Option in Approval
  // stage('Approval') {
            //        steps {
              //  script {
               //     def deploymentDelay = input id: 'Deploy', message: 'Deploy to production?', submitter: 'rkivisto,admin', parameters: [choice(choices: ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9', '10', '11', '12', '13', '14', '15', '16', '17', '18', '19', '20', '21', '22', '23', '24'], description: 'Hours to delay deployment?', name: 'deploymentDelay')]
                //    sleep time: deploymentDelay.toInteger(), unit: 'HOURS'
               // }
         //   }
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
