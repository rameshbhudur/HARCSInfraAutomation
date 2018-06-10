node {
  checkout scm

  stage 'Deploy application Stack'
  //withEnv(["VAULT_PASSWORD=${VAULT_PASSWORD}"]) {
    sh 'ansible-playbook site.yml'
  //}
  //ansiblePlaybook(playbook: 'site.yml', ansibleExecutable: 'venv/bin/ansible-playbook')

}