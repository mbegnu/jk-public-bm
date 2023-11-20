pipeline {
    agent any

    stages {
        stage('Cloning git') {
            steps {
                git branch: 'main', url: 'https://github.com/mbegnu/jk-public-bm.git'
            }
        }
        
        stage('Building image') {
            steps {
                sh 'docker build -t webapp:${BUILD_NUMBER} .'
            }
        }
        
        stage('Deploying the application') {
            steps {
                sh '''
                   docker stop webapp_ctr
                   docker run --rm -d -p 3000:3000 --name webapp_ctr webapp:${BUILD_NUMBER}
                '''
            }
        }
    }
}
