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
                    //archiveArtifacts artifacts: '**/target/*.war' 
                    dir('webapp/target/')
                    {
                        stash name: "maven-build", includes: "*.war"
                    }
                }
            }
            
        }

        stage('Deploy to Dev')
        {
          // when {expression {params.env =='Dev'} beforeAgent true}
            when { expression { params.env == 'Dev' }}
            agent {label "DevServer"}
            steps
            {
                dir('/var/www/html/')
                {
                    unstash "maven-build"
                }

                sh """
                cd /var/www/html/
                java -xvf webapp.war
                """
            }
        }

        satge('Deploy to Prod')
        {
            when {expression {params.env =='Prod'} beforeAgent true}
            agent {label "ProdServer"}
            steps
            {
                timeout(time:5, unit:'Days'){
                    input message: 'Deployment Approved?'
                }
                
                dir('/var/www/html/'){
                    unstach "maven-build"
                }
                sh """
                cd /var/www/html
                java -xvf webapp.war
                """
            }

        }
    }
}