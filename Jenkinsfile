pipeline {
  options {
    ansiColor("xterm")
  }
  agent {
    node {
      label 'master'
    }
  }
  // Code checkout from git.
  stages {
    stage("Lab")
    {
      steps {
        checkout scm
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