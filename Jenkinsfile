pipeline{
    agent any

    tools{
        maven 'localMaven'
    }
    stages{
        stage("Build"){
            steps{
                sh "mvn clean package"
            }
            post{
                success{
                    echo " Build successful"
                    archiveArtifacts artifacts: "**/target/*.war"
                }
                failure{
                    echo " Build failed "
                }
            }
        }
        stage('Deploy to staging'){
            steps{
                timeout(time:5, unit:'DAYS'){
                    input message:'approve production deployment?'
                }
                build job: 'deploy-to-staging'
            }
            post{
                success{
                    echo "Deployed to production"
                }
                failure{
                    echo "Deployment failed"
                }
            }
        }
    }
}