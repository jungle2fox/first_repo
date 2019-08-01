pipeline {
  agent any
  stages {
    stage('build') {
      parallel {
        stage('echo') {
          steps {
            echo 'build stage'
          }
        }
        stage('build a job') {
          steps {
            build 'build job'
            svn(url: 'http://10.0.0.1/svn1', changelog: true)
          }
        }
        stage('build a job') {
          steps {
            build 'aaa'
          }
        }
      }
    }
    stage('test') {
      parallel {
        stage('run script') {
          steps {
            sh '/jsbiz/test.sh'
          }
        }
        stage('sleep') {
          steps {
            sleep 10
          }
        }
      }
    }
    stage('deploy') {
      parallel {
        stage('create zip') {
          steps {
            zip(zipFile: 'ff', archive: true)
          }
        }
        stage('extract files') {
          steps {
            unzip 'ff.tar'
          }
        }
        stage('restart server') {
          steps {
            sh '/jsbiz/start.sh'
          }
        }
      }
    }
  }
}