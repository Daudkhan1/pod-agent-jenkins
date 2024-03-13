node {
    def podYaml = readFile('pod.yaml')

    podTemplate(yaml: podYaml) {
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
