pipeline{
    agent any
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
    }
}