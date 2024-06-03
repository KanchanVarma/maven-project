pipeline{
    agent {
        label "DevServer"
    }

    environment {
        Name = "Kanchan"
    }
    stages
    {
        stage('Build')
        {
            steps{
                echo "This is Build Stage"
                echo "Hi $Name"
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