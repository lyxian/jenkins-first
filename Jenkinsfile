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
                    changes=`echo $(cat tmp.txt) | sed 's/ /\\|/gp'`
                    echo `grep -v "$changes" tmp1.txt`
                    echo "---2---"
                    echo `grep -v $(echo $(cat tmp.txt) | sed 's/ /\\\\|/gp') tmp1.txt`
                    '''
              }
           }
        }
        stage('check_minus') {
            steps {
                script {
                    sh '''
                    grep -n "[-=#]\\*/$" check.txt
                    '''
                }
            }
        }
        stage('git_checkout'){
            steps {
                script{
                    try {
                        gitInfo = git branch: BRANCH_TEST, 
                        url: 'https://github.com/lyxian/jenkins-lib-test'
                    } 
                    catch {
                        branchExist = False
                        echo "${BRANCH_TEST} does not exists"
                    } 
                    finally {
                        if (branchExist == False) {
                            echo "NO"
                        }
                        else {
                            echo "YES"
                        }
                    }
                    echo "$gitInfo"
                }
            }
        }
    }
}