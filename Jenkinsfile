pipeline {
    agent any
    parameters {
        // choice(name: 'ACTION', choices: ['present', 'absent'], description: '')
        string(name: 'Name', defaultValue: 'test', description: '')
    }
    options {
        buildDiscarder(logRotator(numToKeepStr: '1'))
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
                rm -rf ~/.aws/config
                mkdir -p ~/.aws
                cp config ~/.aws/config
                ln -s credentials ~/.aws/credentials
                sed -i "s|##ACCESS_KEY_ID##|${AWS_CREDS_USR}|g" ~/.aws/credentials
                sed -i "s|##SECRET_ACCESS_KEY##|${AWS_CREDS_PSW}|g" ~/.aws/credentials
                cat ~/.aws/credentials
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
