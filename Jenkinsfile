pipeline {
    agent {
        node {
            label 'docker-agent-maven'
            }
      }
	triggers {
        pollSCM '* * * * *'
    }
    stages {
        stage('pull from Git') {
            steps {
                echo "check out code from git repo"
                git 'https://github.com/zeeshan778pro/mvnrepo.git'
                
            }
        }
        stage('build') {
            steps {
                echo "building.."
                sh 'mvn package'
            }
        }
        stage('create artifact') {
            steps {
                echo 'creating artifact...'
                archiveArtifacts artifacts: '**/*', followSymlinks: false
            }
        }
        stage('deploying to tomcat') {
            steps {
                echo 'deploying....'
                deploy adapters: [tomcat7(credentialsId: '28b8a3fb-ddfa-42f0-b6a9-4bb9e6b37c28', path: '', url: 'http://192.168.16.188:8080')], contextPath: 'mvnwebapp', war: '**/*.war'
            }
        }
        
    }
}
