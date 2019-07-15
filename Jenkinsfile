pipeline{
    agent any

    tools{
        maven 'localMaven'
    }

    parameters{
        string(name: 'tomcat_dev', defaultValue: '52.66.164.114', description: 'staging_server')
        string(name: 'tomcat_prod', defaultValue: '13.233.214.137', description: 'production_server')
    }

    triggers{
        pollSCM('* * * * *')
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
        stage('Deployments'){
            parallel{
                stage('Deploy to staging'){
                    steps{
                        sh "scp -i /home/saidalli/Downloads/saidalli.pem **/target/*.war ec2-user@${params.tomcat_dev}:/var/lib/tomcat7/webapps"
                    }
                }
                stage('Deploy to production'){
                    steps{
                        sh "scp -i /home/saidalli/Downloads/saidalli.pem **/target/*.war ec2-user@${params.tomcat_prod}:/var/lib/tomcat7/webapps"
                    }
                }
            }
        }
    }
}