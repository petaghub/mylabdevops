pipeline{
    //Directives
    agent any
    tools {
        maven 'maven'
    }
    environment{
        ArtifactId = readMavenPom().getArtifactId()
        Version = readMavenPom().getVersion()
        Name = readMavenPom().getName()
        GroupId = readMavenPom().getGroupId()
    }


    stages {
        // Specify various stage with in stages

        // stage 1. Build
        stage ('Build'){
            steps {
                sh 'mvn clean install package'
            }
        }

        // Stage 2: Testing
        stage ('Test'){
            steps {
                echo ' testing......'

            }
        }
        // Stage 3 publish to Nexus artifactory
        /*stage('publish artifact to nexus repo'){
            steps{
                nexusArtifactUploader artifacts: [[artifactId: 'mylabDevOps', classifier: '', file: 'target/mylabDevOps-0.0.4-SNAPSHOT.war', type: 'war']], credentialsId: 'b2ccc82a-065e-4055-b007-eab0ca0e9802', groupId: 'com.mylabdevops', nexusUrl: '172.30.10.208:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'mylabDevOps-SNAPSHOT', version: '0.0.4-SNAPSHOT'
            }
        }*/

        // Stage 3 publish to Nexus artifactory
        stage('publish artifact to nexus repo'){
            steps{
                script{

                def NexusRepo = Version.endsWith("SNAPSHOT") ? "mylabDevOps-SNAPSHOT" : "mylabDevOps-RELEASE"
            
                nexusArtifactUploader artifacts: 
                [[artifactId: "${ArtifactId}", 
                classifier: '', 
                file: "target/${ArtifactId}-${Version}.war", 
                type: 'war']], 
                credentialsId: 'b2ccc82a-065e-4055-b007-eab0ca0e9802', 
                groupId: "${GroupId}", 
                nexusUrl: '172.30.10.208:8081', 
                nexusVersion: 'nexus3', 
                protocol: 'http', 
                repository: "${NexusRepo}", 
                version: "${Version}"
                }
            }
        }
        // Stage4 : Print environment variable information
        stage('Print environment variables'){
            steps{
                echo "Artifact ID is '${ArtifactId}'"
                echo "version is '${Version}'"
                echo "Name is '${Name}'"
                echo "GroupId is '${GroupId}'"
                  }
           
        }

        // Stage5 : Publish the source code to Sonarqube
        stage ('Deploy'){
            steps {
                echo ' Deploying......'
                sshPublisher(publishers: 
                [sshPublisherDesc(
                    configName: 'ansible_server', 
                    transfers: [
                        sshTransfer(
                            cleanRemote: false, 
                            execCommand: 'ansible-playbook /opt/playbooks/downloadanddeploy.yaml -i /opt/playbooks/hosts', 
                            execTimeout: 120000, 
                            )], 
                    usePromotionTimestamp: false, 
                    useWorkspaceInPromotion: false, 
                    verbose: false)])
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