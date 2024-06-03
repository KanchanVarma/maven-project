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
                sh 'mvn clean package'
            }
            post{
                success{
                    archiveArtifacts artifacts: '**/target/*.war' 
                }
            }
        }

        stage('test')
        {
            steps{
                echo "This is Test Stage"
            }
        }
    }
}