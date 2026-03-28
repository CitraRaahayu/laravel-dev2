node {

    // ambil source code dari repo
    checkout scm

    // Build stage
    stage('Build') {
        docker.image('php:7.4-cli').inside('-u root') {
            sh 'composer install'
        }
    }

    // Testing stage
    stage('Testing') {
        docker.image('ubuntu').inside('-u root') {
            sh 'echo "Ini adalah test"'
        }
    }
}
