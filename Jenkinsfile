pipeline {
    agent any
    tools {
        maven 'localMaven' 
    }
    stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage ('Deploy to Staging'){
            steps {
                deploy adapters: 
                    [tomcat8(credentialsId: 'tomcat-deployer', path: '', url: 'http://mytomcat:8080')],
                    contextPath: null, war: '**/*.war'
            }
        }
    }
}