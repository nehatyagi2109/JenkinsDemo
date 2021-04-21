pipeline {
    agent any
    tools {
        maven 'maven3'
    }
    stages {
        stage('checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: '76510b6a-26ee-4aa7-8cdb-f0832569d02e', url: 'https://github.com/nehatyagi2109/jenkins-demo.git']]])
                
            }
        }
        
        stage('build') {
            steps {
                sh 'mvn clean install -f MavenProject/pom.xml'
            }
        }
        /* stage('code quality') {
            steps {
                withSonarQubeEnv('Sonarqube'){
                sh 'mvn sonar:sonar -f MavenProject/pom.xml'
            }
        }
    } */
         stage('nexus upload') {
             steps {
                 nexusArtifactUploader artifacts: [[artifactId: 'multi', classifier: '', file: 'MavenProject/multi3/target/multi3-3.7-SNAPSHOT.war', type: 'war']], credentialsId: '9692e8c4-c99d-4494-b194-dd09b67c5ce2', groupId: 'org.jfrog.test', nexusUrl: '3.21.165.142:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'maven-snapshots', version: '3.7-SNAPSHOT'
             }
         }
         stage('Dev Deploy'){
             steps {
                 deploy adapters: [tomcat9(credentialsId: 'a535819b-5fba-412b-87b9-9478a054cc20', path: '', url: 'http://3.141.197.110:8080/')], contextPath: null, war: '**/*.war'
             }
         }
         stage('Slack Notify for Dev deployment'){
             steps {
                 slackSend channel: 'poc', message: 'Dev deployment is successful', teamDomain: 'cicd-4ei9372', tokenCredentialId: '3fe2f4fc-fad2-4865-8292-3d935ea0b58f'
             }
         }
         stage('Dev Approval'){
             steps {
                 echo "Taking approval from Dev Manager for QA deployment"
                 timeout(time: 7, unit:'DAYS'){
                 input message: 'Do you want to deploy into QA environment?', submitter: 'admin'
                 }
             }
         }
         stage('QA Deploy'){
             steps {
                 deploy adapters: [tomcat9(credentialsId: 'a535819b-5fba-412b-87b9-9478a054cc20', path: '', url: 'http://3.141.197.110:8080/')], contextPath: null, war: '**/*.war'
             }
         }
         stage('Slack Notification for QA Deployment'){
             steps {
                 slackSend channel: 'poc', message: 'QA deployment is successful', teamDomain: 'cicd-4ei9372', tokenCredentialId: '3fe2f4fc-fad2-4865-8292-3d935ea0b58f'
             }
         }
}
}
