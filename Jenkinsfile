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
        stage ('Test'){
            steps {
                echo ' testing......'

            }
        }

          // Stage3 : Publish the artifacts to Nexus
        stage ('Publish to Nexus'){
            steps {
                nexusArtifactUploader artifacts: 
                [[artifactId: 'HixDevLab',
                classifier: '', 
                file: 'target/HixDevLab-0.0.2-SNAPSHOT.war', 
                type: 'war']], 
                credentialsId: 'dc6d56c0-9d56-4f90-a098-e2739bbc5daf', 
                groupId: 'de.hixdevlab', 
                nexusUrl: '3.74.154.152:8081', 
                nexusVersion: 'nexus3', 
                protocol: 'http', 
                repository: 'HixDevLab-SNAPSHOT', 
                version: '0.0.2-SNAPSHOT'
            }
        }

        // Stage3 : Publish the source code to Sonarqube
        // stage ('Sonarqube Analysis'){
        //     steps {
        //         echo ' Source code published to Sonarqube for SCA......'
        //         withSonarQubeEnv('sonarqube'){ // You can override the credential to be used
        //              sh 'mvn sonar:sonar'
        //         }

        //     }
        // }

        
        
    }

}