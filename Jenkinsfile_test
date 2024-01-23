pipeline {
    agent {
    kubernetes {
      label 'test-pod'
      defaultContainer 'jnlp'
      yaml """
apiVersion: v1
kind: Pod
spec:
  containers:
  - name: frontend-test
    image: centos:7
    command:
    - cat
    tty: true
    volumeMounts:
    - mountPath: '/opt/app/shared'
      name: sharedvolume
  - name: backend-test
    image: centos:7
    command:
    - cat
    tty: true   
    volumeMounts:
    - mountPath: '/opt/app/shared'
      name: sharedvolume
  volumes:
  - name: sharedvolume
    emptyDir: {}
"""
        }
    }
    stages {
        stage('Test Pipeline Configuration') {
            steps {
                container('frontend-test') {
                    sh 'touch /opt/app/shared/test_file'
                }
                container('backend-test') {
                    sh 'ls /opt/app/shared/test_file ; echo $?'
                }
            }
        }
    }
}