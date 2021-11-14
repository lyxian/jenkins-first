#!groovy

pipeline {
    agent any

    stages {

        stage('first') {
            steps {
                echo "My first build"
                sh "echo `env`"
            }
        }
        stage('test') {
           steps {
              script {
                 sh '''
                  echo -e "a\naa\naaa\nb\nbb" | grep -w "aa\\|aaa"
                 '''
              }
           }
        }
    }
}