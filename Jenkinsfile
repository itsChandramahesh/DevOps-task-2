pipeline {
    agent any

    environment {
        DEPLOY_DIR = "/var/www/html"
        BACKUP_DIR = "/var/backups/website"
    }

    stages {

        stage('Clone Code') {
            steps {
                git branch: 'master' , url: 'https://github.com/itsChandramahesh/DevOps-task-2'
            }
        }

        stage('Backup') {
            steps {
                sh '''
                mkdir -p $BACKUP_DIR
                if [ -d "$DEPLOY_DIR" ]; then
                    cp -r $DEPLOY_DIR $BACKUP_DIR/backup_$(date +%F_%T)
                fi
                '''
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                rm -rf $DEPLOY_DIR/*
                cp -r * $DEPLOY_DIR/
                '''
            }
        }

        stage('Reload Nginx') {
            steps {
                sh 'sudo systemctl reload nginx'
            }
        }
    }
}
