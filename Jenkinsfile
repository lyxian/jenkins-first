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
                  echo "---1---"
                  changes=`echo $(cat tmp.txt) | sed 's/ /\\\\|/gp'`
                  echo `grep -v "$changes" tmp1.txt`
                  echo "---2---"
                  echo `grep -v "echo $(cat tmp.txt) | sed 's/ /\\\\|/gp'" tmp1.txt`
                 '''
              }
           }
        }
    }
}