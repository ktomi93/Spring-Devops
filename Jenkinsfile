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
        stage("Deploy to Staging") {
            steps {
                sh "docker run -d --rm -p 8765:8080 --name calculator ktomi93/devops-pelda"
            }
        }
    }
    post {
        always {
            sh "docker stop calculator"
        }
    }
}
