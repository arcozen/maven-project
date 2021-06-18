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
        stage ('Deploy to Production'){
            steps{
                timeout(time:5, unit:'DAYS'){
                    input message:'Approve PRODUCTION Deployment?'
                }

                deploy adapters: 
                    [tomcat8(credentialsId: 'tomcat-deployer', path: '', url: 'http://mytomcatprod:8080')],
                    contextPath: null, war: '**/*.war'
            }
            post {
                success {
                    echo 'Code deployed to Production.'
                }

                failure {
                    echo ' Deployment failed.'
                }
            }
        }

    }
}