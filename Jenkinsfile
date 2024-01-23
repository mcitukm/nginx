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
  - name: jnlp
    image: jenkins/inbound-agent:latest
    command:
    - cat
    tty: true
    volumeMounts:
    - mountPath: '/opt/app/shared'
      name: sharedvolume
  - name: dind
    image: docker:dind
    command:
    - cat
    tty: true   
    volumeMounts:
    - mountPath: '/opt/app/shared'
      name: sharedvolume
    securityContext:
      privileged: true
  volumes:
  - name: sharedvolume
    emptyDir: {}
"""
        }
    }
    stages {
        stage('Sólo unos comandos linux') {
            steps{
                container('jnlp') {
                    stage('Verificando contenidos') {
                        sh 'cd /opt/app/shared'
                        sh 'touch file'
                        git branch: 'main', url: 'https://github.com/mcitukm/nginx.git'
                        sh '''
                            git version
                            pwd
                            ls -la
                            echo "INFO: git está funcionando ;?"
                        '''
                    }
                }
            }
        }
        stage('Construcción con docker') {
            steps{
                container('dind') {
                    stage('Verificando docker') {
                        sh 'cd /opt/app/shared'
                        //git branch: 'main', url: 'https://github.com/mcitukm/nginx.git'
                        sh '''
                            pwd
                            ls -la
                            docker ps
                            echo "INFO: Docker está funcionando ;?"
                        '''
                    }
                }
            }
        }
    }
}