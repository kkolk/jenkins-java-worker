pipeline {
  options {
    ansiColor("xterm")
  }
  // Code checkout from git.
  stages {
    stage("Lab")
    {
      steps ('Checkout') {
        checkout scm
      }
      steps ('Execute') {
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
}