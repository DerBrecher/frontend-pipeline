#!/usr/bin/env groovy

def templatePath = 'https://raw.githubusercontent.com/DerBrecher/frontend-builder/master/template.json' 
def templateName = 'frontend'

pipeline {
    agent {
        node {
            label 'nodejs'
        }
    }

    options {
        timeout(time: 20, unit: 'MINUTES') 
    }

    stages {
        stage('Preample'){
            steps{
                script {
                    openshift.withCluster() {
                        openshift.withProject() {
                            echo "Using project: ${openshift.project()}"
                        }
                    }
                }
            }
        }
        stage('cleanup') {
            steps {
                script {
                    openshift.withCluster() {
                        openshift.withProject() {
                            echo 'Cleaning up'
                            //openshift.selector("all", [ template : templateName ]).delete() 
                            //if (openshift.selector("secrets", templateName).exists()) { 
                               //openshift.selector("secrets", templateName).delete()                            
                            //}
                        }
                    }
                }
            }
        }
        stage('create') {
            steps {
                script {
                    openshift.withCluster() {
                        openshift.withProject() {
                            openshift.newApp(templatePath) 
                        }
                    }
                }
            }
        }

        stage('Build') {
            steps {
                echo 'Building..'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
                sh 'pwd'
                sh 'oc whoami'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}