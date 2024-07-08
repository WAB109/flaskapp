pipeline {

    agent any

    stages {

        stage('build') {

            when {

                expression {

                    env.GIT_BRANCH == 'origin/master'

                }

            }

            steps {

                echo 'building the application...'

            }

        }

        stage('test') {

            when {

                expression {

                    env.GIT_BRANCH == 'origin/test' || env.GIT_BRANCH == ''

                }

            }

            steps {

                echo 'testing the application...'

            }

        }

        stage('deploy') {

            steps {

                echo 'deploying the application...'

            }

        }

    }

}


