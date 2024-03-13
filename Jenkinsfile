node {
    podTemplate(yaml: readFile('pod.yaml')) {
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
}
