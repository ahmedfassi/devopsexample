pipeline {
    agent any
    tools {
        maven 'Maven3'
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/ahmedfassi/devopsexample.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('MySonarQubeServer') {
                    sh 'mvn sonar:sonar'
                }
            }
        }
        stage('Quality Gate') {
            steps {
                timeout(time: 2, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
        stage('Upload to Nexus') {
            steps {
                nexusArtifactUploader(
                    nexusVersion: 'nexus3',
                    protocol: 'http',
                    nexusUrl: 'nexus:8081',
                    groupId: 'com.devopsexample',
                    version: "0.0.1-${env.BUILD_NUMBER}",
                    repository: 'my-static-site',
                    credentialsId: 'nexus-creds',
                    artifacts: [
                        [artifactId: 'devops', classifier: '', file: 'target/devops-0.0.1-SNAPSHOT.jar', type: 'jar']
                    ]
                )
            }
        }
    }
<<<<<<< HEAD
}
=======
}
>>>>>>> 0d3a8aa87dff004ad830c176211bb8b9f4220393
