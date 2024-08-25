pipeline {
    agent { 
        node {
            label 'ec2-instance'
            }
      }
    triggers {
        pollSCM '* * * * *'
    }

    environment {
      env = "stage"
      namespace = "adi"
    }

    stages {
        stage('Build') {
            steps {
                echo "Building.."
                sh '''
                cd myapp
                pip install -r requirements.txt
                '''
            }
        }
        stage('Test') {
            steps {
                echo "Testing.."
                sh '''
                cd myapp
                python3 hello.py
                python3 hello.py --name=Brad
                '''
            }
        }
        stage('Deliver') {
            steps {
                echo 'Deliver....'
                sh '''
                echo "doing delivery stuff.."
                '''
            }
        }
        stage('Building the image using a dockerfile') {
            agent {
              label 'docker-alpine-python'
            }
            steps {
                sh '''
                docker build -t myappimage:$BUILD_ID .
                '''
            }
        }
    }
}
