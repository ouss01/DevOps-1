pipeline{
    agent any
    
    stages{
       stage ('Git'){
         steps{
              git branch :'main',
              url : 'https://github.com/ouss01/DevOps-1.git',
              credentialsId: 'git_credentials'
              
              }
        }
       stage ('MVN Clean')
        {
         steps{
                sh 'mvn clean install -DskipTests'
            }
        }
         stage ('MVN compile')
        {
         steps{
                sh 'mvn compile'
            }
        }
         stage ('build package')
        {
         steps{
                sh 'mvn clean package'
            }
        }

       

       }    
        
        

    }

