pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('DockerCred') // Credenciales docker hub
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/deividopscba/PruebaDevops.git'
            }
        }

        stage('Build') {
            steps {
                sh 'docker build -t deividopscba/pruebacicdpython .'
            }
        }

        stage('Login to Docker Hub') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }

        stage('Push Docker Image') {
            steps {
                sh 'docker push deividopscba/pruebacicdpython:latest'
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
                    // Ejecutar el contenedor en la máquina anfitriona
                    sh "docker run -d --name pruebacicd_container -p 8000:8000 deividopscba/pruebacicdpython:latest"
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
