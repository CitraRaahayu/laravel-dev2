pipeline {
    agent any

    environment {
        PROD_HOST = "host.docker.internal"
        PROD_USER = "gita"
    }

    stages {

        // stage('Checkout') {
        //     steps {
        //         checkout scm
        //     }
        // }

        stage('Deploy') {
            steps {
                sshagent(['ssh-gita']) {
                    sh '''
                    set -e

                    ssh -o StrictHostKeyChecking=no $PROD_USER@$PROD_HOST << 'EOF'
set -e

cd /home/gita/laravel-dev2 || exit 1

git reset --hard
git clean -fd

git pull origin main

rm -rf vendor
rm -f composer.lock

composer install --no-dev --optimize-autoloader

php artisan migrate --force

php artisan optimize:clear
php artisan config:cache
php artisan route:cache

echo "DEPLOY SUCCESS"
EOF
                    '''
                }
            }
        }
    }
}