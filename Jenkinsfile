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
                        echo "${BAD_CHECKOUT}"
                        // echo "$BAD_CHECKOUT.hudson.AbortException"
                        BAD_CHECKOUT.each { println "Hex Code: $it.key = Color Name: $it.value" }
                        sh '''
                        echo "${BRANCH_TEST} does not exist: ERROR=${BAD_CHECKOUT.hudson.AbortException}"
                        echo "${BRANCH_TEST} does not exist: ERROR=${BAD_CHECKOUT.hudson.AbortException}" > ERROR.txt
                        exit 1
                        '''
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
}