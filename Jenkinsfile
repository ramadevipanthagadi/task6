pipeline {
    agent any

    tools {
        maven 'mymave'
    }

    environment {
        DOCKER_USER = 'sunithriyansh'
        DOCKER_PASS = 'Sunitha@565'
        IMAGE_NAME  = 'roses'
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/ramadevipanthagadi/task6.git'
            }
        }

        stage('Build with Maven') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t roses .'
            }
        }

        stage('Docker Run') {
            steps {
                sh 'docker rm -f cont1 || true'
                sh 'docker run -d --name cont1 -p 8008:8080 roses'
            }
        }

        stage('Push to DockerHub') {
            steps {
                sh 'docker login -u $DOCKER_USER -p $DOCKER_PASS'
                sh 'docker tag imag1:latest $DOCKER_USER/$IMAGE_NAME:latest'
                sh 'docker push $DOCKER_USER/$IMAGE_NAME:latest'
            }
        }

    }
}
stage('Push Docker Image') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                sh 'docker push $DOCKER_IMAGE'
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f k8s/deployment.yml'
                sh 'kubectl apply -f k8s/service.yml'
                sh 'kubectl apply -f k8s/ingress.yml'
            }
        }
    }
}
