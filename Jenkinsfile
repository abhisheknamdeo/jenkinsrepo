pipeline{
    
    agent any
    
    tools{
        // here mymaven is tool configured under global tool configuration
        maven 'mymaven'
    }
    
    stages{
        
        stage('Clone repo')
        
        {
            steps{
                git 'https://github.com/Sonal0409/DevOpsCodeDemo.git'
            }
        }
        
        stage('Compile Code')
        {
            steps{
                // you can have many steps
                sh 'mvn compile'
            }
        }
    
        stage('Code Review'){
            steps{
                sh 'mvn pmd:pmd'
            }
            post {
                success{
                    recordIssues(tools: [pmdParser(pattern: '**/pmd.xml')])
                }
            }
        }
        
          stage('Test Code')
        {
         
            steps{
                // you can have many steps
                sh 'mvn test'
            }
            post{
                success{
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
          stage('Package Code')
        {
            steps{
                // you can have many steps
                sh 'mvn package'
            }
        }
    }
}
