pipeline {
    agent any

    environment {
        PROD_HOST = "host.docker.internal"
        PROD_USER = "gita"
    }

    stages {

        stage('Deploy') {
            steps {
                sshagent(['ssh-gita']) {
                    sh '''
                    set -e

                    ssh -o StrictHostKeyChecking=no $PROD_USER@$PROD_HOST << 'EOF'
set -e

cd /home/gita/laravel-dev2 || exit 1

# Ambil update dari Git
git pull origin main

# Install dependency sesuai composer.lock (STABIL)
composer install --no-dev --optimize-autoloader

# Laravel optimize sequence
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