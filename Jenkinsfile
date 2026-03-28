pipeline {
    agent any

    environment {
        // Jenkins-те сақталған токенді аламыз
        KUBECONFIG_TOKEN = credentials('jenkins-token')
        // Кластердің адресін (Kind болса, әдетте осылай болады)
        K8S_API_URL = "https://kubernetes.default.svc:443"
    }

    stages {
        stage('Setup Helm Repo') {
            steps {
                sh 'helm repo add msvc-repo https://anshelen.github.io/microservices-deploy/'
                sh 'helm repo update'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                // Токенді тікелей Helm командасына қосамыз
                sh """
                helm upgrade --install demo msvc-repo/msvc-chart \
                --namespace demo \
                --set kubeToken=${KUBECONFIG_TOKEN} \
                --kube-apiserver ${K8S_API_URL} \
                --kube-token ${KUBECONFIG_TOKEN} \
                --insecure-skip-tls-verify
                """
            }
        }
    }
    
    post {
        success { echo 'Деплой сәтті аяқталды!' }
        failure { echo 'Қате шықты. Тікелей токен әдісін тексеріңіз.' }
    }
}
