pipeline {
    agent {
        kubernetes {
            yaml '''
apiVersion: v1
kind: Pod
metadata:
  labels:
    some-label: some-value
spec:
  containers:
  - name: build
    image: maven:3.8.1-adoptopenjdk-11
    volumeMounts:
    - name: m2-repo
      mountPath: /root/.m2
    command:
    - cat
    tty: true
  volumes:
  - name: m2-repo
    emptyDir: {}
'''
        }
    }
    options {
        skipStagesAfterUnstable()
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deliver') { 
            steps {
                sh './jenkins/scripts/deliver.sh' 
            }
        }
    }
}
