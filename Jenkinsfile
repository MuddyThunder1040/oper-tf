pipeline {
    agent {
        label 'dell'
    }

    parameters {
        string(name: 'Git-Branch', defaultValue: 'main', description: "Branch to checkout from tf_modules repo")
        string(name: 'TF_Module', defaultValue: 'Local', description: "Terraform Module to run")
        choice(name: 'Terraform-Operation', choices: ['plan', 'apply', 'destroy', 'show'], description: "Terraform operation to run")
    }

    stages {
        stage('Clone Terraform Repo') {
            steps {
                deleteDir()
                git branch: "${params['Git-Branch']}", url: 'https://github.com/MuddyThunder1040/tf_modules.git'
            }
        }

        stage('Run Terraform') {
            steps {
                dir("${params['TF_Module']}") {
                    script {
                        def op = params['Terraform-Operation']
                        sh 'terraform init'

                        if (op == 'plan') {
                            sh 'terraform plan'
                        } else if (op == 'apply') {
                            sh 'terraform apply -auto-approve'
                        } else if (op == 'destroy') {
                            sh 'terraform destroy -auto-approve'
                        } else if (op == 'show') {
                            sh 'terraform show'
                        } else {
                            error "Unsupported Terraform operation: ${op}"
                        }
                    }
                }
            }
        }
    }
}
