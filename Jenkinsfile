pipeline {
    agent any
    
    stages {
        stage('Fetch Repository') {
            steps {
                // Checkout the repository
                checkout scm
            }
        }
        
        stage('Use pod.yaml') {
            steps {
                // Read the content of pod.yaml file
                def podYamlContent = readFile('pod.yaml')
                
                // Output the content of pod.yaml
                echo podYamlContent
                
                // You can use the podYamlContent as needed in your pipeline
                // For example, you can use it in a podTemplate block
                podTemplate(yaml: podYamlContent) {
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
        }
    }
}
