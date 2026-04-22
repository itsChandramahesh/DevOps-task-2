pipeline {
    agent any

    environment {
        DEPLOY_DIR = "/opt/website"
        BACKUP_DIR = "/opt/backup"
    }

    stages {

        stage('Clone Code') {
            steps {
                git 'https://github.com/itsChandramahesh/DevOps-task-2'
            }
        }

        stage('Backup Old Code') {
            steps {
                sh '''
                mkdir -p $BACKUP_DIR
                if [ -d "$DEPLOY_DIR" ]; then
                    cp -r $DEPLOY_DIR $BACKUP_DIR/backup_$(date +%F_%T)
                fi
                '''
            }
        }

        stage('Deploy New Code') {
            steps {
	    sh '''
                rm -rf $DEPLOY_DIR/*
                cp -r * $DEPLOY_DIR/
                '''
            }
        }

        stage('Run Website') {
            steps {
                sh '''
                echo "Deployment Done ✅"


