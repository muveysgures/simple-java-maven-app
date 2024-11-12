pipeline {
    agent any
    environment {
        KOK     = "$WORKSPACE"
        SURUM   = "1.2.$BUILD_ID"
    }
    stage("Git-Pull") {
        steps {
                git branch: "master",
                url: "https://github.com/muveysgures/simple-java-maven-app/tree/master"
        }
    }
    stages {
        stage('Build') { 
            steps {
                sh 'mvn -B -DskipTests clean package' 
            }
        }
    }
}