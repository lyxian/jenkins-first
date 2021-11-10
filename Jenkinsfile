#!groovy

pipeline {
    agent any

    stages {

        stage('first') {
            steps {
                echo "My first build"
            }
        }
        stage('test') {
           steps {
              script {
                 sh '''
                  echo -e "a\naa\naa\nab\nbb" | grep -w "aa\\|aaa"
                 '''
              }
           }
        }
    }
}