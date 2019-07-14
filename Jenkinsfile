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
                build job: 'deploy-to-staging'
            }
        }
    }
}