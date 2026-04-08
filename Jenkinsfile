pipeline {
    agent any

    stages {

        stage('AWS') {
            agent {
                docker {
                    image 'amazon/aws-cli:2.34.26'
                    args "--entrypoint=''"
                }
            }
            environment {
                AWS_S3_BUCKET = 'open-project-bucket-5352'
            }
            steps {
                withCredentials([usernamePassword(credentialsId: 'aws-id', passwordVariable: 'AWS_SECRET_ACCESS_KEY', usernameVariable: 'AWS_ACCESS_KEY_ID')]) {
                sh '''
                aws --version
                aws ecs register-task-definition \
                    --cli-input-json file://aws/task-define.json
      
                '''   
                }
            }
            steps 
        }

    }
}
