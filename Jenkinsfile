pipeline {
  agent any

  parameters {
    booleanParam(name: 'DRY_RUN', defaultValue: true, description: 'semantic-release dry run')
  }

  environment {
    GITHUB_TOKEN = credentials('github-token-id')
    CI = 'true'
  }

  stages {

    stage('Info') {
      steps {
        echo "Branch: ${env.BRANCH_NAME}, DryRun: ${params.DRY_RUN}"
      }
    }

    stage('Install') {
      steps {
        sh '''
          if [ -f package.json ]; then
            npm ci || npm install
          else
            echo "No package.json, skipping install"
          fi
        '''
      }
    }

    stage('Semantic Release') {
      when {
        expression { env.BRANCH_NAME == 'main' || env.BRANCH_NAME == 'develop' }
      }
      steps {
        sh '''
          if [ "${DRY_RUN}" = "true" ]; then
            npx semantic-release --dry-run
          else
            npx semantic-release
          fi
        '''
      }
    }
  }
}
