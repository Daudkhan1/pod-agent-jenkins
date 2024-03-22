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
                    sh """
            set -e
            trivy --cache-dir .trivycache/ image --exit-code 0 --no-progress --input image.tar
            trivy --cache-dir .trivycache/ image --exit-code 1 --ignore-unfixed --severity CRITICAL --no-progress --input image.tar
            """
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
