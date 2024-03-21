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
    image: aquasec/trivy:latest  # Use an image that includes trivy
    command: ["sleep", "infinity"]
  - name: trivy
    image: aquasec/trivy:latest  # Use an image that includes trivy
    command: ["sleep", "infinity"]
  - name: sonarqube
    image: sonarqube:latest
    command: ["sleep", "infinity"] # Adjust as needed

''') {
  node(POD_LABEL) {
    stage('checkout') {
      git 'https://github.com/Daudkhan1/pod-agent-jenkins.git'
    }
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
