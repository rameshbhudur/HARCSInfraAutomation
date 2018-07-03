node {
  checkout scm

  stage 'Deploy two-tier Infrastructure & Application Stack'  
  ansiblePlaybook installation: 'Ansible2.2.0', playbook: '${WORKSPACE}/site.yml'
}
