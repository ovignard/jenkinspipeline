pipeline {
    agent any
    
    stages{
        stage('Buid'){
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving..'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage ('Deploy to Staging'){
            steps{
                build job:'Deploy-to-staging'
            }
        }

        stage ('Deploy to Prouction'){
            steps{
                timeout(time:5,unit:'DAYS'){
                    input message:'Approve PROD deploy?'
                }
                build job:'Deploy-to-prod'
            }
            post{
                success{
                    echo 'Code deployed to Production'
                }
                failure{
                    echo 'Deployment failed'
                }
            }
        }
       
    }
}