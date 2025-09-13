pipeline {
    agent any

    stages {
        stage('Validate Checkout') {
            steps {
                echo 'Code was checked out automatically by Jenkins.'
                sh '''
                ls -la
                cd html_cd
                ls -la
                '''
            }
        }
        
        stage('Testing'){
            steps{
                sh '''
                echo 'testing done'
                '''
            }
        }
        
        stage('Deploy'){
            steps{
                sh '''
                # The ssh command assumes your remote server has access
                # to clone the repository.
                ssh -i ~/.ssh/deploy ubuntu@65.0.45.203 "
                if [ -d 'jenkins' ]; then rm -rf jenkins; fi
                git clone https://github.com/srivatsa-bot/jenkins
                sudo cp jenkins/html_cd/index.html /usr/share/nginx/html
                sudo systemctl restart nginx.service 
                "
                '''
            }
        }
    }
    
    post {
        always {
            // This cleans the workspace on the Jenkins agent
            cleanWs()
        }
    }
}