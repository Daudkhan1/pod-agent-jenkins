podTemplate(containers: [
    containerTemplate(
        name: 'docker', 
        image: 'docker:latest', 
        command: 'sleep', 
        args: '30d'
        ),
    containerTemplate(
        name: 'trivy', 
        image: 'aquasec/trivy:latest', 
        command: 'sleep', 
        args: '30d')
  ]) {

    node(POD_LABEL) {
        stage('image build') {
            git 'https://github.com/Daudkhan1/pod-agent-jenkins.git/'
            container('docker') {
                stage('image build') {
                    sh '''
                    docker build -t myimage .
                    '''
                }
            }
        }

        stage('scan image') {
            git url: 'https://github.com/Daudkhan1/pod-agent-jenkins.git/', branch: 'main'
            container('trivy') {
                stage('scan image') {
                    sh '''
                    trivy image my image
                    '''
                }
            }
        }

    }
}
