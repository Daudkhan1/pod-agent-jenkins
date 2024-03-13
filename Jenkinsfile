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
''') {
  node(POD_LABEL) {
    stage('Get a Maven project') {
      container('jnlp') {
        stage('Shell Execution') {
          sh '''
          echo "Hello! I am executing shell"
          '''
        }
      }
    }
  }
}
