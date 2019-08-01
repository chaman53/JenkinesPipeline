pipeline {
    
    agent any 
    tools {
        maven 'mymaven3.6.1'
    }
        stages {
            stage ('clone') {
                steps {
                  echo " checkout the code from SCM server" 
                  git 'https://github.com/chaman53/jenkinsproject.git'
                  
                }
                
            }
                        stage ('build') {
                steps {
                  echo " compile and package the code" 
                  //git 'https://github.com/chaman53/jenkinsproject.git'
                   sh label: '', script: '''cd /var/lib/jenkins/workspace/Final_project/MavenProject
mvn compile''' 
 sh label: '', script: '''cd /var/lib/jenkins/workspace/Final_project/MavenProject
mvn package'''
                }
                
            }
                    stage ('Archieve Artifacts') {
            steps {
                echo "archiving the artifacts"
                archiveArtifacts 'MavenProject/multi3/target/*.war'
            }
            
        }
                                    stage ('deployment') {
                steps {
                  echo " check tomcat installed or not if not then install and deploy the war file to the tomcat server" 
            //sh label: '', script: ''
            build 'Tomcat_install'
                  echo "deploy the code on tomcat"
                    sh label: '', script: 'sudo rm -rf /Applications/apache-tomcat-7.0.94/webapps/multi3-3.7-SNAPSHOT.war'
                    sh label: '', script: 'sudo cp -r /var/lib/jenkins/workspace/Final_project/MavenProject/multi3/target/multi3-3.7-SNAPSHOT.war /Applications/apache-tomcat-7.0.94/webapps/'
                    //sh label: '',script: 'sudo '
                }
                
            }
                    stage ('publish html report') {
            steps {
                echo "publishing the html report"
                publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: '', reportFiles: 'index.html', reportName: 'HTML Report', reportTitles: ''])
            }
        }
            stage ('Finbugreport') {
                steps {
                sh "mkdir javancss1 ; cd javancss1 ;pwd"
                git 'https://github.com/vathsalahn/jenkins-demo.git'
                    sh "cd javancss-master ; mvn findbugs:findbugs ; pwd"
                     deleteDir()
                }
            }
        }
                   
}
