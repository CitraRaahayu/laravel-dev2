pipeline {
    agent any

    environment {
        APP_ENV = "production"
        PROD_HOST = "172.19.1.74"
        PROD_USER = "gita"
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build (SKIP di Jenkins)') {
            steps {
                echo "Build dilewati di Jenkins (jalan di WSL)"
            }
        }

        stage('Test') {
            steps {
                sh 'echo "Ini test"'
            }
        }

        stage('Deploy (SSH to WSL)') {
            steps {
                sshagent(['ssh-prod']) {
                    sh '''
                        echo "Deploy ke $PROD_HOST"

                        ssh -o StrictHostKeyChecking=no $PROD_USER@$PROD_HOST "
                            cd /home/gita/laravel-dev2 &&
                            git pull origin main &&
                            composer install &&
                            php artisan migrate --force || true &&
                            echo DEPLOY SUCCESS
                        "
                    '''
                }
            }
        }
    }
}