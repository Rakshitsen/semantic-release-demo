pipeline {
  agent any

  environment {
    GITHUB_TOKEN = credentials('github-token-id')
    CI = 'true'
  }

  stages {

    stage('Info') {
      steps {
        echo "Branch detected by Jenkins: ${env.BRANCH_NAME}"
      }
    }

    stage('Install') {
      steps {
        sh 'npm ci || npm install'
      }
    }

    stage('Semantic Release') {
      when {
        expression {
          env.BRANCH_NAME == 'main' || env.BRANCH_NAME == 'develop'
        }
      }
      steps {
        sh 'npx semantic-release'
      }
    }
  }
}
