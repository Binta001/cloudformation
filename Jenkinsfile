pipeline {
    agent any
    parameters {
       choice choices: ['us-east-1a', 'us-east-1b', 'us-east-1c', 'us-east-1d'], name: 'availabilityZone'
       string 'keypair'
       string 'creator'
       string 'region'
       string 'stackname'
   }
    stages {
    
        stage('cloning repo') {
            steps {
            git branch: 'main', url: 'https://github.com/Binta001/cloudformation.git'
            }
        }
        stage('create stack') {
            steps {
                withCredentials([[
                    $class: 'AmazonWebServicesCredentialsBinding',
                    credentialsId: "myaws_cred",
                    accessKeyVariable: 'AWS_ACCESS_KEY_ID',
                    secretKeyVariable: 'AWS_SECRET_ACCESS_KEY'
                ]]) {
                 sh 'aws cloudformation create-stack --stack-name $stackname --template-body file://$WORKSPACE/myDemcf.yml --parameters ParameterKey=mykeypair,ParameterValue=$keypair ParameterKey=az,ParameterValue=$availabiltyZone ParameterKey=creator,ParameterValue=$creator --region $region'
                }
            }
        }
    }
}
