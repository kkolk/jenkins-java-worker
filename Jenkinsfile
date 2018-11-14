pipeline {
  options {
    ansiColor("xterm")
  }
  // Code checkout from git.
  stages {
    stage ('Checkout') {
      checkout scm
    }
    stage ('Execute') {
      // Executing Worker Configuration
      ansiblePlaybook(colorized: true,
        credentialsId: 'ssh-worker',
        inventory: 'inventory/lab/hosts',
        playbook: 'javaworker-install.yml')
      // sudo: true,
      // sudoUser: 'root'
    }
  }
}