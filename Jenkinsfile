pipeline{
    agent {
        label "DevServer"
    }
    
    tools {
        maven 'MyMaven'
    }

    environment {
        Name = "Kanchan"
    }

    parameters {
        choice choices: ['Dev','Prod'], name: 'env'
        string defaultValue: 'Varma', name: 'LastName'
    }
    stages
    {
        stage('Build')
        {
            steps{
                echo "This is Build Stage"
                echo "Hi $Name ${params.LastName}" 
                sh 'mvn clean package -DskipTests=true'
            }
 
        }

        stage('test')
        {
            parallel {
                stage('Unit Test'){
                    agent {
                            label 'DevServer'
                    }
                    steps{
                        echo "This is Unit Test"
                        sh 'mvn test'
                    }
                }
                stage('Intergration Test'){
                    agent {label 'DevServer'}
                    steps{
                        echo "This is Integration Test"
                        sh "mvn test"
                    }
                }
            }
            post{
                success{
                    archiveArtifacts artifacts: '**/target/*.war' 
                }
            }
            
        }
    }
}