helper = new com.freshbooks.jenkinshelper.pipelinehelper()

pipeline {
  agent {
    label 'master'
  }
  options {
    timeout(time: 3, unit: 'MINUTES')
    preserveStashes()
  }
  stages {
    stage('FirstStage') {
      agent {
        label 'master'
      }
      when {
        branch 'master'
        beforeAgent true
      }
      steps {
        script {
          helper.withGithubCredentials {
            sh 'git fetch --all --tags'
            sh 'git checkout -B master'
            println('Test prompt this')
          }
          sh 'ls -al'
          sh 'echo "prompt this"'
        }
      }
    }
    stage('ParallelTest') {
      parallel {
        stage('HelloWorld') {
          agent {
            label 'master'
          }
          stages {
            stage('Hello') {
              steps {
                script {
                  sh 'ls -al'
                  sh 'echo "prompt Hello"'
                }
              }
            }
            stage('World') {
              steps {
                script {
                  sh 'ls -al'
                  sh 'echo "prompt World"'
                }
              }
            }
          }
        }
        stage('Parallel') {
          agent {
            label 'master'
          }
          steps {
            sh "echo 'It is parallel.'"
          }
        }
      }
    }
    stage('Last') {
      agent {
        label 'master'
      }
      steps {
        script {
          sh "echo 'It is the last job.'"
        }
      }
    }
  }
}


