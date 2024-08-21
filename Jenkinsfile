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
                sh 'docker build -t spring-app:v1.02 .'
            }
        }
        stage ('Push Docker image to DockerHub') {
            steps {
                sh 'docker tag spring-app:v1.02 kartikbokade/spring-app:v1.02'
                sh 'docker push kartikbokade/spring-app:v1.02'
            }
        }
        stage ('Send artifact to nexus repository') {
            steps {
                sh 'curl -v -u admin:admin \
    --upload-file ./target/spring-petclinic-2.7.0-SNAPSHOT.jar \
    http://34.229.14.29:8080/repository/spring-snapshot/org/springframework/samples/spring-petclinic-2.7.0-SNAPSHOT.jar'
            }
        }
        stage ('Deploy application on jenkins server') {
            steps {
                sh 'java -jar target/spring-petclinic-2.7.0-SNAPSHOT.jar'
            }
        }
    }
}