pipeline {
    agent any
    stages {
        stage ('Building artifact using maven') {
            steps {
                sh 'mvn --version && mvn install'
                sh 'pwd'
                sh 'ls -la target'
            }
        }
        stage ('Building a docker image') {
            steps {
                sh 'docker build -t spring-app:v1.01 .'
            }
        }
        stage ('Push Docker image to DockerHub') {
            steps {
                sh 'docker tag spring-app:v1.01 kartikbokade/spring-app:v1.01'
                sh 'docker push kartikbokade/spring-app:v1.01'
            }
        }
        stage ('Deploy the application on Jenkins') {
            steps {
                sh 'docker run -d -p 80:8080 --name=spring-container spring-app:v1.01'
                sh 'sleep 10'
                sh 'docker ps'
            }
        }
        stage ('Remove docker images from Jenkins server') {
            steps {
                sh 'docker images && docker rmi kartikbokade/spring-app:v1.01'
            }
        }
    }
}