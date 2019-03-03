pipeline {
  agent {
    label 'docker'
  }
  options {
    timestamps()
    checkoutToSubdirectory 'roles/base'
    ansiColor('xterm')
  }
  stages {
    stage('Prepare') {
      steps {
        // version setup
        script {
          currentBuild.displayName = "1.0.${currentBuild.number}"
        }
      }
    }
    stage('Build') {
      steps {
        ansiblePlaybook(
          playbook: 'build-agent.yml',
          hostKeyChecking: false,
          colorized: true,
          extraVars {
            extraVar("ansible_python_interpreter", "python3", false)
          }
          extras: '-D')
      }
    }
  }
  post {
    always {
      // post version setup ( on failures )
      script {
        currentBuild.displayName = "1.0.${currentBuild.number}"
      }
    }
  }
}
