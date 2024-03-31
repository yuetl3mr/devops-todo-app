#!/usr/bin/env groovy

import groovy.transform.Field

@Field
String SSH_ID_REF = '<SSH_ID_PLACEHOLDER>'

pipeline {
    agent any

    tools {
        dockerTool 'docker'
    }

    stages {
        stage('Build') {
            steps {
                sh 'docker build -t vitnguyen/mgm-training-todo-app:0.0.3 .'
            }
        }
        stage("Docker login and push docker image") {
            steps {
                withBuildConfiguration {
                    sh 'docker login -u "$USER" -p "$PASSWD"'
                    sh 'docker push vitnguyen/mgm-training-todo-app:0.0.3'        		
                }
            }
        }
        stage("deploy") {
             steps {
                 withBuildConfiguration {
                     sshagent(credentials: [SSH_ID_REF]) {
                         sh '''
                            docker run -d --rm --name todo-app -p 8000:8000 vitnguyen/mgm-training-todo-app:0.0.3
                            docker ps
                         '''
                     }
                 }
             }
        }
    }
}

void withBuildConfiguration(Closure body) {
    withCredentials([usernamePassword(credentialsId: DOCKER_USER_REF, usernameVariable: 'repository_username', passwordVariable: 'repository_password')]) {
        body()
    }
    withCredentials([usernamePassword(credentialsId: 'v-docker-hub', usernameVariable: 'USER', passwordVariable: 'PASSWD')]) {
        body()
    }
}

