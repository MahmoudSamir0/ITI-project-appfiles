
pipeline {
    agent { label 'jenkins-agent' }
    stages {
        stage('build') {
            steps {
                script {
                    sh   """
                        docker build -t gcr.io/iti-project-377209/project-iti .
                        docker push gcr.io/iti-project-377209/project-iti
                    """
                }
            }
        }
        stage('deploy') {
            steps {
                script {
                    sh    """
                        kubectl apply -f yaml-files
                    """
                }
            }
        }
    }
}
