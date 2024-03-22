pipeline {
    agent {
        kubernetes {
            yamlFile 'pod.yaml'
        }
    }
    
    stages {
        stage('kaniko build image') {
            steps {
                container('kaniko') {
                   sh 'kaniko --dockerfile=/home/jenkins/agent/workspace/pod-agent-jenkins_main1/Dockerfile --context=/home/jenkins/agent/workspace/pod-agent-jenkins_main1 --destination=daudidrees/my-image:latest'

                }
            }
        }  
        stage('scan image') {
            steps {
                container('trivy') {
                    sh 'trivy image daudidrees/my-image'
                }
            }
        }
        stage('docker run image') {
            steps {
                container ('docker') {
                    sh 'docker run daudidrees/my-image'
                }
            }
        }
    }
}
