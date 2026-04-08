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
                    args "-u root --entrypoint=''"
                }
            }

            steps {
                withCredentials([usernamePassword(credentialsId: 'aws-id', passwordVariable: 'AWS_SECRET_ACCESS_KEY', usernameVariable: 'AWS_ACCESS_KEY_ID')]) {
                sh '''
                yum install jq -y  
                TD_REVISION=$(aws ecs register-task-definition \
                    --cli-input-json file://aws/task-define.json | jq '.taskDefinition.revision')
                echo $TD_REVISION
                aws ecs update-service \
                    --cluster heartfelt-bee-7l0iha \
                    --service learnapp-TaskDefinition-prod-service-hsylsait \
                    --task-definition learnapp-TaskDefinition-prod:$TD_REVISION
      
                '''   
                }
            }
        }

    }
}
