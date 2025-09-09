pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/yourusername/yourrepo.git', branch: 'main'
            }
        }

        stage('Build') {
            steps {
                echo 'Building...'
                // your build commands here
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying using credentials...'
                withCredentials([usernamePassword(credentialsId: '123456789', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    sh "curl -u $USER:$PASS http://yourserver/deploy"
                }
            }
        }
    }
}
