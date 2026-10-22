pipeline {
    agent any

    options {
        skipDefaultCheckout(true)
    }

    environment {
        STUDENT_NAME    = 'Dias'
        STUDENT_SURNAME = 'Adelchanov'
        STUDENT_GROUP   = 'IT2-2313'
        STUDENT_ID      = '37351'
        IMAGE_NAME      = 'adelchanov-dias-devops'
        CONTAINER_NAME  = 'adelchanov-dias-container'
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
                echo "Student: ${STUDENT_NAME} ${STUDENT_SURNAME}"
                echo "Group: ${STUDENT_GROUP}"
                echo "Student ID: ${STUDENT_ID}"
                sh 'chmod +x app/app.sh scripts/Adelchanov_Dias_system.sh'
                sh 'sh -n app/app.sh'
            }
        }
        stage('Test') {
            steps {
                sh './scripts/Adelchanov_Dias_system.sh'
                sh './app/app.sh | grep "Application is running successfully!"'
            }
        }
        stage('Docker Build') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }
        stage('Docker Run') {
            steps {
                sh 'docker rm -f $CONTAINER_NAME || true'
                sh '''
                    docker run --name $CONTAINER_NAME \
                      -e STUDENT_NAME=$STUDENT_NAME \
                      -e STUDENT_SURNAME=$STUDENT_SURNAME \
                      -e STUDENT_GROUP=$STUDENT_GROUP \
                      -e STUDENT_ID=$STUDENT_ID \
                      $IMAGE_NAME
                '''
            }
        }
    }
}
