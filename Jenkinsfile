pipeline {
    agent {
        kubernetes {
            yamlFile 'pod.yaml'
        }
    }
    
    stages {
        // stage('kaniko build image') {
        //     steps {
        //         container('kaniko') {
        //             // sh 'cat /home/jenkins/agent/workspace/kaniko-build@tmp/durable-ebf05f3f/script.sh.copy'
        //            sh 'kaniko --dockerfile=/home/jenkins/agent/workspace/pod-agent-jenkins_main1/Dockerfile --context=/home/jenkins/agent/workspace/pod-agent-jenkins_main1 --destination=daudidrees/my-image:latest'

        //         }
        //     }
        // }  

         stage('Build docker image') {
      steps {
        container(name: 'kaniko') {
          sh """
          executor -c=$WORKSPACE/ -f=$WORKSPACE/Dockerfile --cleanup --no-push --destination image --tarPath image.tar
          """
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
