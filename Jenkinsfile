pipeline {
    agent any
    
    stages{
        stage('Buid'){
            steps {
                sh 'mvn clean package'
            }
            post{
                success{
                    echo 'Now Archivining'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage('Deploy to Staging')
    }
}