node {
  checkout scm

  stage 'Deploy Infrastructure & Application Stack'  
  ansiblePlaybook installation: 'Ansible2.2.0', playbook: '${WORKSPACE}/site.yml'
}
