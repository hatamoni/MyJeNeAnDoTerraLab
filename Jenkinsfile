pipeline{
    //Directives
    agent any
    tools {
        maven 'maven'
    }

    environment {
       ARTIFACTID = readMavenPom().getArtifactId()
       VERSION = readMavenPom().getVersion()
       NAME = readMavenPom().getName()
       GROUPID = readMavenPom().getGroupId()
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
        stage ('Test'){
            steps {
                echo ' testing......'
            }
        }

          // Stage3 : Publish the artifacts to Nexus
        stage ('Publish to Nexus'){
            steps {
                    script {

                    def NexusRepo = Version.endsWith("SNAPSHOT") ? "HixDevLab-SNAPSHOT" : "HixDevLab-RELEASE"

                    nexusArtifactUploader artifacts: 
                    [[artifactId: "${ArtifactId}", 
                    classifier: '', 
                    file: "target/${ArtifactId}-${Version}.war", 
                    type: 'war']], 
                    credentialsId: 'dc6d56c0-9d56-4f90-a098-e2739bbc5daf', 
                    groupId: "${GroupId}",  
                    nexusUrl: '3.74.154.152:8081', 
                    nexusVersion: 'nexus3', 
                    protocol: 'http', 
                    repository: "${NexusRepo}",
                    version: "${Version}"
                }
            }
        }
        
        // Stage 4 : Print some information
        stage ('Print Environment variables'){
                    steps {
                        echo "Artifact ID is '${ARTIFACTID}'"
                        echo "Version is '${VERSION}'"
                        echo "GroupID is '${GROUPID}'"
                        echo "Name is '${NAME}'"
                    }
        }    
    }
}
