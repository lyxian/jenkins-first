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
                  x="a\naa\naa\nab\nbb\n"
                  echo -e $x | grep -w "aa|aaa"
                 '''
              }
           }
        }
    }
}