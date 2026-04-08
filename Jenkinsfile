pipeline {
    agent any

    stages {

        stage ('AWS') {
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
                aws --version
      
                '''   
                }
            }
        }

    }
}
