pipeline {
    agent any
    stages {
        stage('Deploy') {
            steps {
                sh 'helm upgrade --install demo microservices/microservices-deploy --namespace demo'
            }
        }
    }
}
