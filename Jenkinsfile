pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "maven_ph"
    }

    stages {
        stage('Gitcheckout') {
            steps {
              git credentialsId: 'git_cred', url: 'https://github.com/PhaniSekhar4/maven_Webexample.git' 
            }
        }
        stage('build') {
            steps {
              bat 'mvn clean install'
            }
        }
        stage('codeQuality') {
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
