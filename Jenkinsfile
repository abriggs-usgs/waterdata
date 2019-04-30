pipeline {
  agent {
    node {
      label 'project:any'
    }
  }
  parameters {
    choice(choices: ['development', 'staging', 'production'], description: 'deployment environment', name: 'DEPLOY_TIER')
  }
  stages {
    stage('Build') {
      agent {
        dockerfile {
          args '-u root:root -v "${WORKSPACE}":/src -e "HUGO_BASEURL=/labs.waterdata.usgs.gov" -e  "HUGO_VERSION=0.55.4" '
          reuseNode true
        }
      }
      steps {
        sh "/src/entrypoint.sh build"
      }
    }
  }
}
