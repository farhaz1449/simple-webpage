pipeline {
    agent any
    
    environment {
        DEPLOY_IP = '13.220.9.193' // Replace with Instance B IP
    }

    stages {
        // Only use that portion of the code when not using SCM and code is in the script in Jenkins url
        // stage('Checkout') {
        //     steps {
        //         // Jenkins downloads your code from GitHub
        //         git branch: 'main', url: 'https://github.com/farhaz1449/simple-webpage.git'
        //     }
        // }

        stage('Test') {
            steps {
                echo 'Validating index.html...'
                // Simple test: Ensure the word "Welcome" exists in your code
                sh 'grep -q "Abu Farhaz" index.html'
            }
        }

        stage('Deploy') {
            steps {
                sshagent(['ssh-key-access']) {
                    echo "Deploying to Web Server..."
                    // Copy all files from the repository to Instance B
                    sh "scp -r -o StrictHostKeyChecking=no ./* ubuntu@${DEPLOY_IP}:/var/www/html/"
                }
            }
        }
    }
}
