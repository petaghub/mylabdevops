pipeline{
    //Directives
    agent any
    tools {
        maven 'maven'
    }

    stages {
        // Specify various stage with in stages

        // stage 1. Build
        stage ('Build'){
            steps {
                sh 'mvn clean install package'
            }
        }

        // Stage2 : Testing
        /*stage ('Test'){
            steps {
             nexusArtifactUploader artifacts: [[artifactId: 'VinayDevOpsLab', classifier: '', file: '/var/lib/jenkins/workspace/PiplelineJob/target/VinayDevOpsLab-0.0.12.war', type: 'war']], credentialsId: '6db65c96-4eb9-40d6-804a-610e9afc0ab8', groupId: 'com.vinaysdevopslab', nexusUrl: '172.20.10.148:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'VinaysDevOpsLab-SNAPSHOT', version: '0.0.12'

            }
        }*/
        // Stage 2: Testing
        stage ('Test'){
            steps {
                echo ' testing......'

            }
        }
        // Stage 3 publish to Nexus artifactory
        stage('publish artifact to nexus repo'){
            steps{
                nexusArtifactUploader artifacts: [[artifactId: 'mylabDevOps', classifier: '', file: 'target/mylabDevOps-0.0.4-SNAPSHOT.war', type: 'war']], credentialsId: 'b2ccc82a-065e-4055-b007-eab0ca0e9802', groupId: 'com.mylabdevops', nexusUrl: '172.30.10.208:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'mylabDevOps-SNAPSHOT', version: '0.0.4-SNAPSHOT'
            }
        }

        // Stage4 : Publish the source code to Sonarqube
        stage ('Deploy'){
            steps {
                echo ' Deploying......'
                
                }

            }
            
        // Stage4 : Publish the source code to Sonarqube
        //stage ('Sonarqube Analysis'){
          //  steps {
            //    echo ' Source code published to Sonarqube for SCA......'
              //  withSonarQubeEnv('sonarqube'){ // You can override the credential to be used
                //     sh 'mvn sonar:sonar'
                //}

            //}
        //}

        
        
    }

}