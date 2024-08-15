pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/deividopscba/PruebaDevops.git'
            }
        }

        stage('Build') {
            steps {
                script {
                    dockerImage = docker.build("deividopscba/pruebacicdpython")
                }
            }
        }

        stage('Test') {
            steps {
                sh 'docker run --rm pruebacicdpython python manage.py test'
            }
        }

        stage('Deploy') {
            steps {
                script {
                    dockerImage.push('latest')
                }
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}