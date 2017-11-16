pipeline {
    agent any
    stages {
        stage("Checkout") {
            steps {
                git url: "https://github.com/ktomi93/Spring-Devops.git"
            }
        }
        stage("Packaging") {
            steps {
                sh "./gradlew build"
            }
        }
        stage("Docker build") {
            steps {
                sh "docker build -t ktomi93/devops-pelda ."
            }
        }
        stage("Docker login") {
            steps {
                sh "docker login --username ktomi93 --password=$docker_password"
            }
        }
        stage("Docker push") {
            steps {
                sh "docker push ktomi93/devops-pelda"
            }
        }
        stage("Deploy to Production") {
            steps {
                sh "ansible-playbook playbook.yml -i inventory/production"
            }
        }
    }
}
