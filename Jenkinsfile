node {

    environment {
        APP_ENV = "production"
        PROD_HOST = "127.0.0.1"
    }

    stage('Checkout') {
        checkout scm
    }

    stage('Build') {
        docker.image('composer:2').inside('-u root') {
            sh 'composer install'
        }
    }

    stage('Test') {
        docker.image('ubuntu').inside('-u root') {
            sh 'echo "Ini test"'
        }
    }

    stage('Deploy (SSH)') {
        sshagent(['ssh-prod']) {
            sh '''
                echo "Deploy ke $PROD_HOST"
                ssh -o StrictHostKeyChecking=no root@$PROD_HOST "echo DEPLOY LARAVEL-DEV2 JALAN"
            '''
        }
    }
}