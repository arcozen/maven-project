pipeline {
    agent none

    stages {
        stage('Build') {
            agent {label 'master'}
            steps {
                echo 'Building..'
            }
        }
        stage('Test') {
            agent {label 'master'}
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            agent {label 'master'}
            steps {
                echo 'Deploying....'
            }
        }
    }
}