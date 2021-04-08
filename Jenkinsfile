pipeline {
    agent any
    tools {
        maven 'maven3'
        jdk 'JDK8'
    }
    parameters {
        string(name: 'version', defaultValue: '', description: 'version to deploy the file on prod')
        choice(name: 'environment', choices: ['uat1', 'uat2'], description: 'choices for environment')
        booleanParam(name: 'executetest, defaultValue: true, description: '')
    }
    stages {
        stage('build') {
            steps {
                echo "building maven project...."
              
            }
        }
        stage('test') {
            when {
                expression {
                    params.executetest == true
                }
            }
            steps {
                echo "testing maven build.."
                echo "testing version ${version}"
              
            }
        }
    }
}
