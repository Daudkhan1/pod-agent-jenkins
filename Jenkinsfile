podTemplate(label: 'kubeagent', yaml: '''
apiVersion: v1
kind: Pod
metadata:
  labels:
    jenkins: agent
  name: my-pod
spec:
  containers:
  - name: jnlp
    image: jenkins/inbound-agent:latest
  - name: docker
    image: aquasec/trivy:latest
    command: ["sleep", "infinity"]
  - name: trivy
    image: aquasec/trivy:latest
    command: ["sleep", "infinity"]
  - name: sonarqube
    image: sonarqube:latest
    command: ["sleep", "infinity"]
''') {
  node('kubeagent') {
    stage('Get a Maven project') {
      container('docker') {
        stage('Shell Execution') {
          sh '''
          trivy image jenkins/jenkins
          '''
        }
      }
    }
  }
}
