pipeline {
    agent { label 'testnode' }
// Updated slave server label
    stages {
        stage('Pull Code') {
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
    }
}
