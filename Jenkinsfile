node {
    // Print current workspace directory
    echo "Current workspace: ${pwd()}"

    // Print the list of files in the workspace directory
    sh 'ls -al'

    // Read the pod.yaml file
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
