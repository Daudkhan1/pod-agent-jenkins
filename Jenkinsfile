pipeline {
    agent {
        kubernetes {
            yaml '''
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
spec:
  containers:
    - name: jnlp
      image: jenkins/inbound-agent:alpine-jdk17
      command:
        - "/bin/sh"
        - "-c"
      args:
        - "while ! /usr/local/bin/jenkins-slave ; do sleep 5 ; done"
      resources:
        limits:
          cpu: 500m
          memory: 250Mi
        requests:
          cpu: 500m
          memory: 250Mi
    - name: goldenalgo
      image: registry-acdc.tools.msi.audi.com/goldenalgo-build-agent:1.6.1
      # hack to keep container running. see
      # https://github.com/jenkinsci/kubernetes-plugin#constraints
      command:
        - cat
      tty: true
      resources:
        limits:
          cpu: 2
          memory: 6Gi
        requests:
          cpu: 2
          memory: 4Gi
      volumeMounts:
        - name: ivy2-credentials
          mountPath: /root/.ivy2/.credentials
          subPath: .credentials
    - name: elasticsearch-server
      image: registry-acdc.tools.msi.audi.com/elasticsearch:7.10.2
      ports:
        - containerPort: 9200
      resources:
        limits:
          cpu: 2
          memory: 3Gi
        requests:
          cpu: 1
          memory: 1Gi
      env:
        - name: discovery.type
          value: "single-node"
    - name: kaniko
      image: registry-acdc.tools.msi.audi.com/kaniko:debug-v1.3.0-1
      command:
        - cat
      resources:
        limits:
          cpu: 1
          memory: 2Gi
        requests:
          cpu: 1
          memory: 1Gi
      tty: true
      volumeMounts:
        - name: docker-config
          mountPath: /kaniko/.docker/
    - name: trivy
      image: registry-acdc.tools.msi.audi.com/trivy:0.36.1
      env:
        - name: TRIVY_OFFLINE_SCAN
          value: "true"
      command:
        - cat
      resources:
        limits:
          cpu: 2
          memory: 3Gi
        requests:
          cpu: 0.5
          memory: 500Mi
      tty: true
      volumeMounts:
        - name: docker-config
          mountPath: /root/.docker/
        - name: workspace
          mountPath: /workspace
  volumes:
    - name: docker-config
      configMap:
        name: nexus-config
    - name: kaniko-secret
      secret:
        secretName: acdc-registry
    - name: ivy2-credentials
      configMap:
        name: ivy2-credentials
    - name: workspace
      emptyDir: {}
  imagePullSecrets:
    - name: acdc-registry
  restartPolicy: Never
            '''
        }
    }
    stages {
        stage('Get a Maven project') {
            steps {
                container('jnlp') {
                    stage('Shell Execution') {
                        sh 'echo "Hello! I am executing shell"'
                    }
                }
            }
        }
    }
}

