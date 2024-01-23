podTemplate(containers: [
    containerTemplate(
        name: 'jnlp', 
        image: 'jenkins/inbound-agent:latest'
    ),
    containerTemplate(
        name: 'docker',
        image: 'docker:dind'
    )
  ]) {
    node(POD_LABEL) {
        stage('Sólo unos comandos linux') {
            container('jnlp') {
                stage('Verificando contenidos') {
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
        stage('Construcción con docker') {
            container('jnlp') {
                stage('Verificando docker') {
                    //git branch: 'main', url: 'https://github.com/mcitukm/nginx.git'
                    sh '''
                        docker ps
                        echo "INFO: Docker está funcionando ;?"
                    '''
                }
            }
        }
    }
}