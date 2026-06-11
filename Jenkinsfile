pipeline {
    agent none

    stages {

        stage('Debug') {
            agent any
            steps {
                echo "BRANCH_NAME = ${env.BRANCH_NAME}"
                echo "GIT_BRANCH = ${env.GIT_BRANCH}"
            }
        }

        stage('TEST Branch') {
            when {
                expression {
                    env.GIT_BRANCH?.contains('test')
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
	
	stage('PROD Branch') {
            when {
                expression {
                    env.GIT_BRANCH?.contains('prod')
                }
            }

            agent {
                label 'prodnode'
            }

            steps {
                sh '''
                mkdir -p ~/git-content

                if [ ! -d ~/git-content/.git ]; then
                    git clone -b prod https://github.com/awsarchitect2030/Jenkins_GIT_work.git ~/git-content
                else
                    cd ~/git-content
                    git pull origin prod
                fi
                '''
            }
        }

        stage('DEVELOP Branch') {
            when {
                expression {
                    env.GIT_BRANCH?.contains('develop')
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
    }
}
