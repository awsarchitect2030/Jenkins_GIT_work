pipeline {
    agent none

    stages {

        stage('Debug') {
            agent any
            steps {
                echo "JOB_NAME    = ${env.JOB_NAME}"
                echo "BRANCH_NAME = ${env.BRANCH_NAME}"
                echo "GIT_BRANCH  = ${env.GIT_BRANCH}"
            }
        }

        stage('DEVELOP Branch') {
            when {
                expression {
                    env.JOB_NAME == 'MoveAutomationJob'
                }
            }

            agent {
                label 'myslave_label'
            }

            steps {
                sh '''
                mkdir -p ~/git-content

                if [ ! -d ~/git-content/.git ]; then
                    git clone -b develop https://github.com/awsarchitect2030/Jenkins_GIT_work.git ~/git-content
                else
                    cd ~/git-content
                    git pull origin develop
                fi
                '''
            }
        }

        stage('Trigger TEST Job') {
            when {
                expression {
                    env.JOB_NAME == 'MoveAutomationJob'
                }
            }

            steps {
                build job: 'Push to test', wait: true
            }
        }

        stage('TEST Branch') {
            when {
                expression {
                    env.JOB_NAME == 'Push to test'
                }
            }

            agent {
                label 'testnode'
            }

            steps {
                sh '''
                mkdir -p ~/git-content

                if [ ! -d ~/git-content/.git ]; then
                    git clone -b test https://github.com/awsarchitect2030/Jenkins_GIT_work.git ~/git-content
                else
                    cd ~/git-content
                    git pull origin test
                fi
                '''
            }
        }

        stage('Trigger PROD Job') {
            when {
                expression {
                    env.JOB_NAME == 'Push to test'
                }
            }

            steps {
                build job: 'Push to Prod', wait: true
            }
        }

        stage('PROD Branch') {
            when {
                expression {
                    env.JOB_NAME == 'Push to Prod'
                }
            }

            agent {
                label 'prodnode'
            }

            steps {
                sh '''
                mkdir -p ~/git-content

                if [ ! -d ~/git-content/.git ]; then
                    git clone -b master https://github.com/awsarchitect2030/Jenkins_GIT_work.git ~/git-content
                else
                    cd ~/git-content
                    git pull origin master
                fi
                '''
            }
        }
    }
}
