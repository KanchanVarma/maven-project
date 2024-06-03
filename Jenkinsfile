pipeline{
    agent {
        label "DevServer"
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