pipeline{
    //Directives
    agent any
    tools {
        maven 'maven'
    }

    environment {
        ArtifactId = readMavenPom().getArtifactId()
        GroupID = readMavenPom().getGroupId()
        Version = readMavenPom().getVersion()

        }

    stages {
        // Specify various stage with in stages

        // stage 1. Build
        stage ('Build'){
            steps {
                sh 'mvn clean install package'
            }
        }

        // Stage2 : Publish the source code to Nexus
        stage ('Publish to Nexus'){
            steps {
                script{
                    def NexusRepo = Version.endsWith("SNAPSHOT") ? "ManisDevOpsLab-SNAPSHOT":"ManisDevOpsLab-RELEASE"
                nexusArtifactUploader artifacts: 
                [
                    [artifactId: "${ArtifactId}",
                    classifier: '', 
                    file: "target/${ArtifactId}-${Version}.war", 
                    type: 'war']], 
                    credentialsId: 'ae9cb28a-cac6-4817-ba40-7f2bac65b8c3', 
                    groupId: "${GroupId}", 
                    nexusUrl: '13.59.169.237:8081', 
                    nexusVersion: 'nexus3', 
                    protocol: 'http', 
                    repository: "${NexusRepo}", 
                    version: "${Version}"
                }
                }

            }
        }

        
        
    }