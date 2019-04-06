pipeline {
    agent any
    stages{
        stage('---CLEAN---'){
            steps {
                sh 'mvn clean'
            }
        }
        stage('---TEST---'){
            steps {
               sh 'mvn test'
            }
        }
    }
}
