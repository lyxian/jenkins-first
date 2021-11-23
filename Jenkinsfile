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
                  ls
                  cat tmp.txt
                  > tmp.txt
                  cat tmp.txt
                  echo "d\ne" > tmp.txt
                  cat tmp.txt
                 '''
              }
           }
        }
    }
}