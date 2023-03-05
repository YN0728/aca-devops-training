pipeline { 
    agent any
    
    environment {
        WEB_HOSTNAME = "bnglo.zapto.org"
        WEB_URL = "https://${WEB_HOSTNAME}"
        DOCKERHUB_USERNAME = "nydocker28"
        DOCKERHUB_PASSWORD = credentials("docker-password")
        IMAGE_TAG = "1.0.1"
    }
    stages {
        stage('Prepare') {
            steps {
                sh "docker login -u ${DOCKERHUB_USERNAME} -p ${DOCKERHUB_PASSWORD}"
            }
        }
        stage('Build Frontend') {
            environment {
                REACT_APP_API_BASE_URL = "${WEB_URL}/api"
            }
            steps {
                dir("applications/frontend-react") {
                    sh "ls -la"
                    sh "docker build -t ${DOCKERHUB_USERNAME}/frontend-react:${IMAGE_TAG} --build-arg REACT_APP_API_BASE_URL=${REACT_APP_API_BASE_URL} ."
                    sh "docker push ${DOCKERHUB_USERNAME}/frontend-react:${IMAGE_TAG}"
                }
            }
        }
        stage('Build Backend') {
            steps {
                // sh "docker login -u ${DOCKERHUB_USERNAME} -p ${DOCKERHUB_PASSWORD}"
                echo 'yeeey'
            }
        }
        // stage('Deploy') {
        //     environment {
        //         DEV_SERVER_IP = "167.71.36.251"
        //         // SERVER_IP = BRANCH_NAME == "develop" ? DEV_SERVER_IP : PROD_SERVER_IP
        //     }
        //     steps {
        //         withCredentials([sshUserPrivateKey(credentialsId: "droplet-ssh-key", keyFileVariable: 'KEY_FILE')]) {
        //             sh 'ssh -o StrictHostKeyChecking=no -i ${KEY_FILE} root@${DEV_SERVER_IP} "cd /root/frontend && export IMAGE_TAG=${IMAGE_TAG} && docker compose pull && docker compose up -d"'
        //         }
        //     }   
        // }
    }
}
