node {
  checkout scm

  stage 'Deploy application Stack'
  ansiblePlaybook installation: 'Ansible2.2.0', playbook: '${WORKSPACE}/site.yml'
}
