//Pipeline project for clone build archive and deploy to tomcat server
//Author: Kaushal Chaman
//Version : v1.00
pipeline {
    agent any
     tools {
        maven 'Maven3'
        }
    stages {
         stage('clone') {
            steps {
                echo "clone git repo"
                sh "pwd"
                git credentialsId: '3a146c91-2ae4-4d59-86d1-8829836673be', url: 'https://github.com/chaman53/jenkinsproject.git'
            }
         }
            stage('build') {
            steps {
                   echo "compiling the code"
                   //sh label: '', script: 'pwd'
                   //sh label: 'jenkins', script: 'ip a'
                   //sh label: '', script: "'cd /var/lib/jenkins/workspace/Pipeline_project/MavenProject mvn compile"'
                      sh label: '', script: '''cd /var/lib/jenkins/workspace/Pipeline_project/MavenProject
mvn compile'''   
                           }
            }
                        stage('archive') {
            steps {
                   echo "create package the code"
                   //sh label: '', script: 'pwd'
                   //sh label: 'jenkins', script: 'ip a'
                   //sh label: '', script: "'cd /var/lib/jenkins/workspace/Pipeline_project/MavenProject mvn compile"'
                      sh label: '', script: '''cd /var/lib/jenkins/workspace/Pipeline_project/MavenProject
mvn package'''   
                           }
            }
                                    stage('tomcat&Install&Deploy') {
            steps {
                   echo "Checking tomcat install or not if not then deploy the tomcat"
                   build 'Tomcat_install'
                    echo "deploy the code on tomcat"
                      
                           }
            }
    }
}
