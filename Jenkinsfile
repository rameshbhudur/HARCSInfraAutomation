node {
  checkout scm

  stage 'Deploy application Stack'
  //withEnv(["VAULT_PASSWORD=${VAULT_PASSWORD}"]) {
    sh '/home/ec2-user/ansible/bin/ansible/ansible-playbook site.yml'
  //}
  //ansiblePlaybook 'site.yml'
}