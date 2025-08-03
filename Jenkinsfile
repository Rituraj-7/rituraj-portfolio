pipeline {
    agent any

    environment {
        REPO_URL = 'https://github.com/Rituraj-7/rituraj-portfolio.git'
        BRANCH = 'main' // adjust if you're using 'master'
        DOCKER_IMAGE = 'grunner/rituraj-portfolio'
        TAG = 'latest'
        K8S_DEPLOYMENT = 'portfolio-deployment'
        KUBECONFIG_CREDENTIAL_ID = 'kubeconfig' // if using Jenkins credentials plugin
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: "${BRANCH}", url: "${REPO_URL}"
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t ${DOCKER_IMAGE}:${TAG} .'
                }
            }
        }

        stage('Push to DockerHub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    script {
                        sh """
                            echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                            docker push ${DOCKER_IMAGE}:${TAG}
                        """
                    }
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                script {
                    sh """
                        kubectl set image deployment/${K8S_DEPLOYMENT} portfolio=${DOCKER_IMAGE}:${TAG} --record
                    """
                }
            }
        }
    }

    post {
        success {
            echo ' Deployment successful!'
        }
        failure {
            echo ' Error!'
        }
    }
}
