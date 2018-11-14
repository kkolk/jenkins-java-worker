node () {
  // Code checkout from git.
  stage ('Checkout') {
    checkout scm
  }
  stage ('Execute') {
    // Executing Worker Configuration
    ansiblePlaybook colorized: true,
    credentialsId: 'ssh-worker',
    limit: "${HOST_PROVISION}",
    installation: 'ansible',
    inventory: 'inventory/lab/hosts',
    playbook: 'javaworker-install.yml',
    sudo: true,
    sudoUser: 'root'
  }
}
