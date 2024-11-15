pipeline {
    agent any
    
     environment {
        ORGANIZATION_NAME = "muhammadadel8"
        DOCKERHUB_USERNAME = "muhammadadel8"
        REPOSITORY_TAG = "${DOCKERHUB_USERNAME}/${ORGANIZATION_NAME}-${SERVICE_NAME}:${BUILD_ID}"
    }
       
   stages {
       stage ('git checkout') {
           steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']],userRemoteConfigs: [[url: 'https://github.com/MuhammadAdel612/test.git']]])
           }
       }
    
       
        stage ('Build and Push Image') {
            steps {
                   sh 'docker build -t ${REPOSITORY_TAG} .'
                   sh 'docker push ${REPOSITORY_TAG}'          
            }
          }
       }
       
       stage ('Deploy to Cluster') {
            steps {
                sh " kubectl apply -f pod.yml"
                }
            }
}
}
