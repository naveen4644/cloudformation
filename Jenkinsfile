pipeline {
    agent any

    environment {
        AWS_REGION = 'us-east-1'  // Specify the AWS region
        STACK_NAME = 'DEMO'  // Specify the CloudFormation stack name
        TEMPLATE_FILE = 'devops/demo.yml'  // Specify the CloudFormation template file
      //  PARAMETER_FILE = 'parameters.json'  // Specify the CloudFormation parameter file
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/naveen4644/cloudformation.git'
            }
        }

        stage('Deploy CloudFormation Stack') {
            steps {
                script {
                    // Deploy CloudFormation stack
                    def ssmParamName = '/desamist/aws/account/ENV' // Update with your parameter name
                    def s3Bucket = sh(script: "aws ssm get-parameter --name ${ssmParamName} --query Parameter.Value --output text", returnStdout: true).trim()
                    echo "Retrieved S3 Bucket: ${s3Bucket}"
                    
                    sh 'aws cloudformation deploy --template-file ${TEMPLATE_FILE} --stack-name ${s3Bucket} --capabilities CAPABILITY_IAM --region ${AWS_REGION}'
                }
            }
        }
    }
}

