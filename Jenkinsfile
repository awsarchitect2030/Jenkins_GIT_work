pipeline {
    agent any

    stages {
        stage('Pull Code') {
            steps {
                sh '''
             #   mkdir -p /home/ec2-user/git-content

                if [ ! -d /home/ec2-user/git-content/.git ]; then
                    git clone -b develop https://github.com/awsarchitect2030/Jenkins_GIT_work.git /home/ec2-user/git-content
                else
                    cd /home/ec2-user/git-content
                    git pull origin develop
                fi
                '''
            }
        }
    }
}
