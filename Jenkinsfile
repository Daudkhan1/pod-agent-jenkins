pipeline {
    agent {
        kubernetes {
            yaml '''
                apiVersion: v1
                kind: Pod
                metadata:
                  name: my-pod
                spec:
                  containers:
                  - name: jnlp
                    image: jenkins/inbound-agent:latest
                  - name: docker
                    image: docker:latest
                    command: ["sleep", "infinity"]
                  - name: trivy
                    image: aquasec/trivy:latest
                    command: ["sleep", "infinity"]
                  - name: sonarqube
                    image: sonarqube:latest
                    command: ["sleep", "infinity"] # Adjust as needed
            '''
            label POD_LABEL
        }
    }
    stages {
        stage('Get a Maven project') {
            steps {
                container('jnlp') {
                    sh 'echo "Hello! I am executing shell"'
                }
            }
        }
    }
}
