node {
  checkout scm

  stage 'Deploy application Stack'
  //withEnv(["VAULT_PASSWORD=${VAULT_PASSWORD}"]) {
    sh '/usr/local/bin/ansible/ansible-playbook site.yml'
  //}
  //ansiblePlaybook 'site.yml'
}
