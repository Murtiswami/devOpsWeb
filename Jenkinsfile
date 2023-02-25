pipeline {
    agent any
    
    tools {
        maven 'LocalMaven'
    }
    environment {
        fname = "Ranjit"
        lname = "Swain"
        version = "1.2"
        system = "Dev"
    }

stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Archiving the artifacts'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

        stage ('Deployments'){
            parallel{
                stage ('Deploy to Staging'){
                    steps {
                        
                        echo "This is made by ${env.fname} ${env.lname}"
                        echo "it's running on ${env.system} and the version is ${env.version}"
                       deploy adapters: [tomcat7(credentialsId: 'abe63ae6-7b40-4683-a9dd-9fc195c3db0f', path: '', url: 'http://13.233.214.80:8282/')], contextPath: null, war: '**/*.war'
                 }
                }

                stage ("Deploy to Stagin2"){
                    steps {
                        echo 'This is just a demo on Production server.'
                        /*script{
                            props = readProperties file: 'build.cnf'
                        }
                        echo "Current Version ${props['deploy.version']}"*/
                    }
                }
            }
        }
    }
}
