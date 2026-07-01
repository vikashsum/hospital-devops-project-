pipeline {
    agent any

    parameters {
        choice(name: 'ENVIRONMENT', choices: ['dev'], description: 'Terraform environment')
        choice(name: 'ACTION', choices: ['plan', 'apply', 'destroy'], description: 'Pipeline action')
        booleanParam(name: 'AUTO_APPROVE', defaultValue: false, description: 'Auto approve apply/destroy')
    }

    environment {
        AWS_DEFAULT_REGION = 'ap-south-1'
        TF_IN_AUTOMATION   = 'true'
        TF_INPUT           = 'false'
        TF_DIR             = "terraform/envs/${params.ENVIRONMENT}"
        BACKEND_FILE       = "../../backend/${params.ENVIRONMENT}.hcl"
        TFVARS_FILE        = "${params.ENVIRONMENT}.tfvars"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Terraform Version') {
            steps {
                sh 'terraform version'
                sh 'aws --version'
                sh 'kubectl version --client || true'
            }
        }

        stage('Terraform Fmt') {
            steps {
                sh 'terraform fmt -recursive -check'
            }
        }

        stage('Terraform Init') {
            steps {
                dir("${env.TF_DIR}") {
                    sh 'terraform init -backend-config=${BACKEND_FILE} -reconfigure'
                }
            }
        }

        stage('Terraform Validate') {
            steps {
                dir("${env.TF_DIR}") {
                    sh 'terraform validate'
                }
            }
        }

        stage('Terraform Plan') {
            when {
                anyOf {
                    expression { params.ACTION == 'plan' }
                    expression { params.ACTION == 'apply' }
                }
            }
            steps {
                dir("${env.TF_DIR}") {
                    sh 'terraform plan -var-file=${TFVARS_FILE} -out=tfplan'
                }
            }
        }

        stage('Approval') {
            when {
                expression {
                    (params.ACTION == 'apply' || params.ACTION == 'destroy') && !params.AUTO_APPROVE
                }
            }
            steps {
                input message: "Approve ${params.ACTION} for ${params.ENVIRONMENT}?", ok: 'Approve'
            }
        }

        stage('Terraform Apply') {
            when {
                expression { params.ACTION == 'apply' }
            }
            steps {
                dir("${env.TF_DIR}") {
                    sh 'terraform apply -auto-approve tfplan'
                }
            }
        }

        stage('Configure Kubeconfig') {
            when {
                expression { params.ACTION == 'apply' }
            }
            steps {
                dir("${env.TF_DIR}") {
                    script {
                        env.CLUSTER_NAME = sh(
                            script: 'terraform output -raw cluster_name',
                            returnStdout: true
                        ).trim()
                    }
                }

                sh 'aws eks update-kubeconfig --region ${AWS_DEFAULT_REGION} --name ${CLUSTER_NAME}'
                sh 'kubectl get nodes'
            }
        }

        stage('Deploy App to EKS') {
            when {
                expression { params.ACTION == 'apply' }
            }
            steps {
                sh 'kubectl apply -f kubernetes/'
                sh 'kubectl get pods -n hospital'
                sh 'kubectl get svc -n hospital'
            }
        }

        stage('Terraform Destroy') {
            when {
                expression { params.ACTION == 'destroy' }
            }
            steps {
                dir("${env.TF_DIR}") {
                    sh 'terraform destroy -var-file=${TFVARS_FILE} -auto-approve'
                }
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: "${env.TF_DIR}/tfplan", allowEmptyArchive: true
        }
    }
}