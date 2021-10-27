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

        // Stage3 : Publish the source code to Nexus
        stage ('Publish to Nexus'){
            steps {
                nexusArtifactUploader artifacts: 
                [
                    [artifactId: 'ManisDevOpsLab',
                    classifier: '', 
                    file: 'target\\ManisDevOpsLab-0.0.2-SNAPSHOT.war', 
                    type: 'war']], 
                    credentialsId: 'ae9cb28a-cac6-4817-ba40-7f2bac65b8c3', 
                    groupId: 'com.manidevopslab', 
                    nexusUrl: '13.59.169.237:8081', 
                    nexusVersion: 'nexus3', 
                    protocol: 'http', 
                    repository: 'ManisDevopsLab-SNAPSHOT', 
                    version: '0.0.3-SNAPSHOT'
                }

            }
        }

        
        
    }