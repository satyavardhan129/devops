pipeline {
    agent {
        node {
            label 'java11'
        }
    
    }

    options {
                timestamps()
                buildDiscarder(logRotator(numToKeepStr: '2', artifactNumToKeepStr: '2'))
                timeout(time: 240, unit: 'MINUTES')
                disableConcurrentBuilds()
                }

        stages {
            stage ('AppCodeCheckout') {
                steps {

                    git 'https://github.com/gcpcloudreddy/pylife-devops-demo.git'

                }
            }
            stage ('CI Build') {

                steps {

                    sh 'mvn clean package'
                   
                     }
    
            }

            stage ('Docker Build && Push && RUN ') {
               
                steps {
                    sh 'docker build . -t pylifedevops/app29:test'
                    sh 'docker login -u pylifedevops -p dckr_pat_DCaoHJYadQolqu3KkrNOhDEnbr8'
                    sh 'docker push pylifedevops/app29:test'
                    sh 'docker run -p 89:8080 -d pylifedevops/app29:test'
                }
            
        }
    }

}