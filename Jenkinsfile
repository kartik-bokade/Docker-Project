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
                sh 'docker build -t spring-app:v1.1 .'
                sh 'docker images'
            }
        }
        stage ('Push Docker image to DockerHub') {
            steps {
                sh 'docker tag spring-app:v1.1 kartikbokade/spring-app:v1.1'
                sh 'docker push kartikbokade/spring-app:v1.1'
                sh 'docker images'
            }
        }
        stage ('Remove docker images from Jenkins server') {
            steps {
                sh 'docker images && docker rmi kartikbokade/spring-app:v1.01'
            }
        }
    }
}