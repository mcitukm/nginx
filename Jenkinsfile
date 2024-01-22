podTemplate(containers: [
    containerTemplate(
        name: 'jnlp', 
        image: 'jenkins/inbound-agent:latest'
    )
  ]) {

    node(POD_LABEL) {
        stage('Just a shell command') {
            container('jnlp') {
                stage('Checking contents') {
                    git branch: 'main', url: 'https://github.com/mcitukm/nginx.git'
                    sh '''
                        git version
                        pwd
                        ls -la
                        echo "token is working"
                    '''
                }
            }
        }

    }
}