pipeline {

  agent {
    node {
      label 'master'
    }
  }

  options {
    timestamps()
  }

  stages {
    stage('PHPUnit Test') {
      steps {
        echo 'Running PHPUnit...'
        sh '/bin/phpunit ${WORKSPACE}'
      }
    }
    stage('Merge PR') {
      when {
        branch 'PR-*'
      }
      steps {
        sh 'git remote set-url origin git@github.com:practicaljenkins/phptest.git' /* changing url for ssh git access*/
        sh 'git remote set-branches --add origin ${CHANGE_TARGET}' /* by default source branch will be used we need to change it  */
        sh 'git fetch origin' /* fetching the target branch */
        sh 'git checkout ${CHANGE_TARGET}' /* checking out the target branch */
        sh 'git merge --no-ff ${GIT_COMMIT}' /* merging the revision of  target branch */
        sh 'git push origin ${CHANGE_TARGET}'
      }
    }
  }
}

