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
         stage ('SonarQube :Quality Test')
            {
            steps{
                 withSonarQubeEnv(installationName: 'sonar'){
                    sh 'mvn sonar:sonar'
                }
                }
            }
       stage("Publish to Nexus Repository Manager") {
                   steps {
                        nexusArtifactUploader artifacts: [
                            [
                                artifactId: 'achat',
                                classifier: '',
                                file: 'target/achat-1.0.jar',
                                type: 'jar']],
                            credentialsId: 'Devops',
                            groupId: 'tn.esprit.rh',
                            nexusUrl: '192.168.1.12:8081',
                            nexusVersion: 'nexus3',
                            protocol: 'http',
                            repository: 'achat-realeases',
                            version: '1.0'
                   }
                     }

         stage('Docker image'){
                    steps {
                         sh 'docker build -t oussematr/springapp .'
                    }
                }

         stage('DockerCompose') {

                    steps {

         				            sh 'docker compose up -d'
                          }

                 }

          stage('push to DockerHub'){
                     steps {
         		   withCredentials([string(credentialsId: 'dockerHub1-id', variable: 'dockerhubpwd')]) {
                             sh 'docker login -u ousstrimech -p ${dockerhubpwd}'
                             sh 'docker push oussematr/springapp'

                         }
                }
                }
       }



    }

