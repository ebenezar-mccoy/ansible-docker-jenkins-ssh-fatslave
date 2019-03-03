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
          extras: '-D',
          extraVars: [
            ansible_python_interpreter: 'python3'
          ]
          )
      }
    }
  }
  post {
    always {
      // debugger
      sleep 300
      // post version setup ( on failures )
      script {
        currentBuild.displayName = "1.0.${currentBuild.number}"
      }
    }
  }
}
