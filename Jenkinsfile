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
        stage('Stage 1 - IP Info') {
            steps {
                sh 'echo "IP Info:"'
                sh 'hostname -I || ip addr show'
            }
        }
        stage('Stage 2 - CPU Info') {
            steps {
                sh 'echo "CPU Info:"'
                sh 'lscpu || cat /proc/cpuinfo'
            }
        }
        stage('Stage 3 - Memory Info') {
            steps {
                sh 'echo "Memory Info:"'
                sh 'free -h || cat /proc/meminfo'
            }
        }
        stage('Stage 4 - Disk Usage') {
            steps {
                sh 'echo "Disk Usage:"'
                sh 'df -h'
            }
        }
        stage('Stage 5 - Uptime') {
            steps {
                sh 'echo "Uptime:"'
                sh 'uptime'
            }
        }
        stage('Stage 6 - OS Info') {
            steps {
                sh 'echo "OS Info:"'
                sh 'cat /etc/os-release'
            }
        }
        stage('Stage 7 - Network Interfaces') {
            steps {
                sh 'echo "Network Interfaces:"'
                sh 'ip link show'
            }
        }
        stage('Stage 8 - Running Processes') {
            steps {
                sh 'echo "Running Processes:"'
                sh 'ps aux --sort=-%mem | head -n 10'
            }
        }
        stage('Stage 9 - Open Ports') {
            steps {
                sh 'echo "Open Ports:"'
                sh 'ss -tuln || netstat -tuln'
            }
        }
        stage('Stage 10 - Environment Variables') {
            steps {
                sh 'echo "Environment Variables:"'
                sh 'printenv'
            }
        }
    }
}