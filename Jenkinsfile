properties([pipelineTriggers([githubPush()])])

pipeline {
  agent {
    docker {
      image 'docker build . -t ansible_lespagnol'
      args '--entrypoint='
    }

  }

  stages {
    stage('Launch playbook') {
      steps {
        sh 'ansible-playbook -i inventory install.yml'
      }
    }
  }

  environment {
    AWS_REGION = 'eu-west-3'
  }

  options {
    withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'ynov_20', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']])
  }
}
