pipeline {
    agent none

    stages {
        stage('TEST Branch') {
            when {
                branch 'test'
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

        stage('DEVELOP Branch') {
            when {
                branch 'develop'
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
