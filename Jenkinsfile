pipeline {
    agent any
    stages {
        stage ('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: 'refs/heads/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '35cccb33-e523-42b6-9c1d-d1aaa475ffbe', url: 'git@github.com:uladzimirkrul/jenkins-homework']]])
        
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
                success {
                    echo 'successful test'
                }
            }
        }
        stage('Deploy') {
            steps {
                sshagent(credentials: ['tomcat-ssh']) {
                    sh "scp -o StrictHostKeyChecking=no **/*.war tomcat@192.168.10.234:~latest/webapps"
                }
            }
        }
    }
}
