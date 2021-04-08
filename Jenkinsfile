pipeline {
    agent any
    tools {
        maven 'maven3'
        jdk 'JDK8'
    }
    stages {
        stage('build') {
            steps {
                echo "building maven project...."
                sh 'mvn compile'
            }
        }
        stage('test') {
            steps {
                echo "testing maven build.."
                sh 'mvn test'
            }
        }
    }
}
