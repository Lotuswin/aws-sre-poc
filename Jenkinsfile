pipeline {
    agent none
    parameters {
        // choice(name: 'ACTION', choices: ['present', 'absent'], description: '')
        string(name: 'Name', defaultValue: 'test', description: '')
    }
    options {
        buildDiscarder(logRotator(numToKeepStr: '10'))
        disableConcurrentBuilds()
        timestamps()
        // ansiColor('xterm')
    }
    stages {
        stage('EC2 Deploy') {
            // agent {
            //     label none
            // }
            environment {
                AWS_CREDS=credentials('aws-secrets')
            }
            steps {
                sh """
                set -ex
                mkdir -p ~/.aws
                cp config ~/.aws/
                sed -i "s|##ACCESS_KEY_ID##|${AWS_CREDS_USR}|g" ~/.aws/config
                sed -i "s|##ACCESS_KEY_ID##|${AWS_CREDS_PASS}|g" ~/.aws/config
                cat ~/.aws/config
                aws s3 ls
                #terraform init
                #terraform apply -auto-approve
                #terraform destroy -auto-approve
                """
            }
            // when {
            //     branch ''
            //     not {
            //         changeRequest()
            //     }
            // }
        }
    }
}