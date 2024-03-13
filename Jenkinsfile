def podYaml = readFile('pod.yaml')

podTemplate(yaml: podYaml) {
  node('mypod') {
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
