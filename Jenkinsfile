pipeline {
  agent {
    label 'docker'
  }
  environment {
    NEXUS_CREDENTIALS = credentials('2db9a2f5-7838-4646-9477-37b1a9236e5d')
    NEXUS_USER = "${env.NEXUS_CREDENTIALS_USR}"
    NEXUS_PASS = "${env.NEXUS_CREDENTIALS_PSW}"
  }
  options {
    timestamps()
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
        // withCredentials([usernamePassword( credentialsId: '2db9a2f5-7838-4646-9477-37b1a9236e5d',
        // passwordVariable: 'DOCKER_PASS', usernameVariable: 'DOCKER_USER')]) {
        //   sh "export ANSIBLE_DOCKER_USER=${env.DOCKER_USER}"
        //   sh "export ANSIBLE_DOCKER_USER=${env.DOCKER_PASS}"
        // }
        ansiblePlaybook(
          playbook: 'build-agent.yml',
          hostKeyChecking: false,
          colorized: true,
          extras: '-D -v',
          extraVars: [
            ansible_python_interpreter: 'python3',
            image_tag: "$BUILD_DISPLAY_NAME",
            nexus_user: [value: "$NEXUS_USER", hidden: true],
            nexus_password: [value: "$NEXUS_PASS", hidden: true]
          ]
        )
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
