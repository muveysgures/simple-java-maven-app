pipeline {
    agent any
    environment {
        KOK     = "$WORKSPACE"
        SURUM   = "1.2.$BUILD_ID"
    }
    stages {
        stage('Git-Pull') {
            steps {
                git branch: "master",
                ur: "https://github.com/muveysgures/simple-java-maven-app/tree/master"
            }
        }
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Docker-Build') {
            steps {
                sh " docker image build -t app.jar:latest . "
                sh " docker run app-jar:latest "
            }
        }
    }
}