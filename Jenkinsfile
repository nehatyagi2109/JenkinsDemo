pipeline {
    agent any
    tools {
        maven 'maven3'
        jdk 'JDK8'
    }
    parameters {
        choice(name: 'environment', choices: ['uat1', 'uat2'], description: 'choices for environment')
        booleanParam(name: 'executeTest, defaultValue: true, description: '')
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
                    params.executeTest == true
                }
            }
            steps {
                echo "testing maven build.."
                echo "testing environment ${environment}"
              
            }
        }
    }
}
