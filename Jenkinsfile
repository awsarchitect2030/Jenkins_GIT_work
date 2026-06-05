pipeline {
    agent myslave

    stages {
        stage('Pull Code') {
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
