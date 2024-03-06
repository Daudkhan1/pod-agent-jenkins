pipeline {
    agent {
        label 'kubeagent'  // Using the label for the Kubernetes pod template
    }
    stages {
        stage('Install kubectl') {
            steps {
                script {
                    // Download and install kubectl
                    sh 'curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl'
                    sh 'chmod +x kubectl'
                    sh 'mv kubectl /usr/local/bin/kubectl'
                }
            }
        }
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
