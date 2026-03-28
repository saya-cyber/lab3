pipeline {
    agent any

    environment {
        // Jenkins-те құрған Secret text-тің ID-і осы жерде болуы керек
        KUBECONFIG_TOKEN = credentials('jenkins-token')
    }

    stages {
        stage('Setup Helm Repo') {
            steps {
                // Репозиторийді қосу және жаңарту
                sh 'helm repo add msvc-repo https://anshelen.github.io/microservices-deploy/'
                sh 'helm repo update'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                // Дұрыс команда: репозиторий/чарт_аты
                // Егер бұрын токенмен проблема болса, осы жерде қолданылады
                sh 'helm upgrade --install demo msvc-repo/msvc-chart --namespace demo'
            }
        }
    }
    
    post {
        success {
            echo 'Деплой сәтті аяқталды!'
        }
        failure {
            echo 'Қате шықты. Логтарды тексеріңіз.'
        }
    }
}
