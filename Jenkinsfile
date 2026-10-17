pipeline {
    agent any
    environment {
        STUDENT_NAME    = 'Bekassyl'
        STUDENT_SURNAME = 'Zholdas'
        STUDENT_GROUP   = 'SE-2306'
        STUDENT_ID      = '37350'
        IMAGE           = 'zholdas-bekassyl-devops'
        CONTAINER       = 'zholdas-bekassyl-container'
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
                sh 'git log -1 --oneline'
            }
        }
        stage('Build') {
            steps {
                sh 'chmod +x app/app.sh scripts/Zholdas_Bekassyl_system.sh'
                sh 'echo "Student: $STUDENT_NAME $STUDENT_SURNAME"; echo "Group: $STUDENT_GROUP"; echo "Student ID: $STUDENT_ID"'
            }
        }
        stage('Test') {
            steps {
                sh 'test -f Zholdas_Bekassyl_info.txt'
                sh 'sh -n app/app.sh'
                sh './scripts/Zholdas_Bekassyl_system.sh'
            }
        }
        stage('Docker Build') {
            steps {
                sh 'docker build -t $IMAGE .'
            }
        }
        stage('Docker Run') {
            steps {
                sh 'docker rm -f $CONTAINER || true'
                sh 'docker run --name $CONTAINER -e STUDENT_NAME -e STUDENT_SURNAME -e STUDENT_GROUP -e STUDENT_ID $IMAGE'
            }
        }
    }
}
