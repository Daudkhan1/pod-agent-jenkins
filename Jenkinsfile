podTemplate(yaml: '''
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
''') {
  node(POD_LABEL) {
    stage('Get a Maven project') {
      container('docker') {
        stage('Shell Execution') {
          sh '''
          docker build -t myimage .
          '''
        }
      }
    }
  }
}
