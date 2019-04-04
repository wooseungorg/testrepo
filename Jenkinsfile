pipeline {
  agent {
    label 'master'
  }
  options {
    timeout(time: 2, unit: 'MINUTES')
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
          steps {
            script {
              sh 'ls -al'
              sh 'echo "prompt Hello"'
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
          sh "echo 'It is the last JOB!'"
        }
      }
    }
  }
}
