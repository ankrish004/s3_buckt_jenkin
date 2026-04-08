pipeline {
    agent any
    environment {
        AWS_DEFAULT_REGION = 'us-east-1'
    }

    stages {

        stage ('AWS-cli') {
            agent {
                docker {
                    image 'amazon/aws-cli:2.34.26'
                    args "--entrypoint=''"
                }
            }

            steps {
                withCredentials([usernamePassword(credentialsId: 'aws-id', passwordVariable: 'AWS_SECRET_ACCESS_KEY', usernameVariable: 'AWS_ACCESS_KEY_ID')]) {
                sh '''
 
                aws ecs register-task-definition \
                    --cli-input-json file://aws/task-define.json

                aws ecs update-service \
                    --cluster heartfelt-bee-7l0iha \
                    --service learnapp-TaskDefinition-prod-service-hsylsait \
                    --task-definition learnapp-TaskDefinition-prod:2
      
                '''   
                }
            }
        }

    }
}
