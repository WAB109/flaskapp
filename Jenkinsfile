pipeline {

    agent any

    parameters {

        choice(name: 'VERSION', choices: ['1.1.0', '1.2.0', '1.3.0'], description: 'Select the version to deploy')

        booleanParam(name: 'executeTests', defaultValue: true, description: 'Execute Tests')

    }

    stages {

        stage("init") {

            steps {

                script {

                    gv = load "script.groovy"

                }

            }

        }

        stage("Checkout") {

            steps {

                checkout scm

            }

        }

        stage("Build") {

            steps {

                // Corrected Docker build command

                sh "docker build -t flask-jenkins:${params.VERSION} ."

            }

        }

        stage("test") {

            when {

                expression {

                    params.executeTests

                }

            }

            steps {

                script {

                    gv.testApp()

                }

            }

        }

        stage("Tag and Push") {

            steps {

                withCredentials([[$class: 'UsernamePasswordMultiBinding',

                credentialsId: 'docker-hub', 

                usernameVariable: 'DOCKER_USER_ID', 

                passwordVariable: 'DOCKER_USER_PASSWORD'

                ]]) {

                    sh "docker tag flask-jenkins:${params.VERSION} ${DOCKER_USER_ID}/jenkins-app:${params.VERSION}"

                    sh "docker login -u ${DOCKER_USER_ID} -p ${DOCKER_USER_PASSWORD}"

                    sh "docker push ${DOCKER_USER_ID}/jenkins-app:${params.VERSION}"

                }

            }

        }

        stage("deploy") {

            steps {

                echo 'deploying the application...'

            }

        }

    }

}


