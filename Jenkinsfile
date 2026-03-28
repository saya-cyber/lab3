pipeline {
    agent any

    stages {
        stage('Setup Helm Repo') {
            steps {
                sh 'helm repo add msvc-repo https://anshelen.github.io/microservices-deploy/'
                sh 'helm repo update'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                // KUBECONFIG айнымалысы арқылы файлды тікелей көрсетеміз
                sh 'KUBECONFIG=/var/jenkins_home/config-k8s helm upgrade --install demo msvc-repo/msvc-chart --namespace demo'
            }
        }
    }
    
    post {
        success { echo 'Деплой сәтті аяқталды!' }
        failure { echo 'Қате шықты. Файл жолын немесе рұқсаттарды тексеріңіз.' }
    }
}
