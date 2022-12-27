pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'master',
                        credentialsId: '35cccb33-e523-42b6-9c1d-d1aaa475ffbe',
                        url: 'ssh://git@github.com:uladzimirkrul/jenkins-homework.git'
                sh "ls -lat"
            }
        }
        stage('Build') {
            steps {
                sh 'mvn -f pom.xml -B -DskipTests clean package'
            }
            post {
                success {
                    echo 'Success build'
                }
            }
        }
        stage('Test') {
            steps {
                sh 'mvn -f pom.xml test'
            }
            post {
                always {
                    junit '/target/surefire-reports/*.xml'
                }
            }
        }
    }
}
