pipeline {
    agent any
    tools {
        maven "maven_ph"
    }
    stages {
        stage('git checkout') {
            steps {
            git branch: 'main', credentialsId: 'jen_cred', url: 'https://github.com/PhaniSekhar4/maven_Webexample.git'
            }
            
        }
        stage ('build') {
            steps{
                bat 'mvn clean install'
            }
        }
        stage ('code quality') {
            steps {
                bat 'mvn sonar:sonar'
            }
        }
        stage('deploy') {
            steps {
                deploy adapters: [tomcat8(credentialsId: 'tomcat_cred', path: '', url: 'http://localhost:8085/')], contextPath: 'pipelineProject', war: '**/*.war'
            }
        }
       
    }
}