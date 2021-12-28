#!groovy

def gitInfo = {}
def branchExists = "True"

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
        stage('git_checkout'){
            steps {
                script{
                    try {
                        gitInfo = git branch: BRANCH_TEST, 
                        url: 'https://github.com/lyxian/jenkins-first'
                        // echo "$gitInfo"
                        writeFile file: 'tmp', text: "$gitInfo"
                        echo "File Saved"
                    } 
                    catch (BAD_CHECKOUT) {
                        // env.ERR_MSG = BAD_CHECKOUT
                        // echo "${BAD_CHECKOUT}"
                        echo "${BRANCH_TEST} does not exist: ERROR=${BAD_CHECKOUT}"
                        writeFile file: 'ERROR.txt', text: "${BRANCH_TEST} does not exist: ERROR=${BAD_CHECKOUT}"
                        // err = sh(script: "echo ${env.ERR_MSG} | cut -d ':' -f2-", returnStdout: true).toString().trim()
                        // sh '''
                        // echo "${BRANCH_TEST} does not exist: ERROR=${BAD_CHECKOUT.hudson.AbortException}"
                        // echo "${BRANCH_TEST} does not exist: ERROR=${BAD_CHECKOUT.hudson.AbortException}" > ERROR.txt
                        // echo "${ERR_MSG}"
                        // exit 1
                        // '''
                        ERROR = sh(script: "cat ERROR.txt", returnStdout: true).toString().trim()
                        error "${BRANCH_TEST} does not exist: ERROR=${BAD_CHECKOUT}"
                        // branchExists = ""
                        // echo "${BRANCH_TEST} does not exist: ${err}"
                    } 
                    echo "HELLO, IM STILL HERE. IF YOU PASS"
                    // finally {
                    //     if (branchExists) {
                    //         echo "YES"
                    //     }
                    //     else {
                    //         sh 'exit 1'
                    //     }
                    // }
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
        // emailext body: 'ZXC', subject: 'ASD', to: 'lyxlyxi@hotmail.com'
    }
    post {
        always {
            script {
                // echo "${ERR_MSG}"
                // ERROR = sh(script: "cat ERROR.txt", returnStdout: true).toString().trim()
                sh '''
                ls -ltr
                # echo `env`
                '''
                // echo "${ERROR}"
                // sh 'cat ERROR.txt'
                // cleanWs()
            }
        }
        success {
            echo "NO ERROR"
            // emailext body: 'TEST', subject: 'SUCCESS', to: 'lyxlyxi@hotmail.com'
        }
        failure {
            echo "$ERROR"
            // emailext body: 'TEST', subject: 'FAILURE', to: 'lyxlyxi@hotmail.com'
        }
    }
}