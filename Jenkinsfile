pipeline {
    agent {
        node {
            label 'java11'
        }
    
    }

    options {
                timestamps()
                buildDiscarder(logRotator(numToKeepStr: '5', artifactNumToKeepStr: '2'))
                timeout(time: 240, unit: 'MINUTES')
                disableConcurrentBuilds()
                }

        stages {
            stage ('AppCodeCheckout') {
                steps {

                    git 'https://github.com/satyavardhan129/devops.git'

                }
            }
            stage ('CI Build') {

                steps {

                    sh 'mvn clean package'
                   
                     }
    
            }

            stage ('Docker Build && Push && DEPLOY ') {
               

                steps {
                     
                    sh 'docker build . -t satyavardhan129/demo29:latest '
                    sh 'docker login -u satyavardhan129 -p dckr_pat_rDGKM9Tj1XraOUGr2qfKslzrPZ4 '
                    sh 'docker push satyavardhan129/demo29:latest'
                    sh 'docker run -p 89:8080 -d satyavardhan129/demo29:latest'
                

                }
            
        }

        }

            
         
}
