pipeline {
    agent {
        label 'kubeagent'  // Using the label for the Kubernetes pod template
    }
    stages {
        stage('Create Pod on Kubernetes') {
            steps {
                script {
                    // Define pod YAML
                    def podYaml = '''
                        apiVersion: v1
                        kind: Pod
                        metadata:
                          name: my-pod
                        spec:
                          containers:
                          - name: my-container
                            image: nginx
                    '''
                    
                    // Create the pod on Kubernetes
                    sh """
                        echo '$podYaml' > my-pod.yaml
                        kubectl apply -f my-pod.yaml
                    """
                }
            }
        }
    }
}
