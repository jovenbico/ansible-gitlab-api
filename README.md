# Ansible playbook - Gitlab API

## Delete pipeline per project
```
$ ansible-playbook \
  --extra-vars "project_id=** private_token=** updated_before=$(date -d '30 days ago' -u +'%Y-%m-%dT%H:%M:%SZ')" \
  delete-pipeline.yml
```

## Run script with cron
```
$ sudo apt install cron
$ crontab -e

## every 3rd minute ##
*/3 * * * *  ansible-playbook --extra-vars "project_id=** private_token=** updated_before=2022-07-19T00:00:00Z" /workspaces/gitlab-cleanup/delete-pipeline.yml >> /workspaces/gitlab-cleanup/output.txt

$ sudo service cron start
```

### Reference
https://docs.ansible.com/ansible/2.9/user_guide/playbooks_delegation.html#local-playbooks  
https://docs.gitlab.com/ee/user/gitlab_com/index.html#gitlabcom-specific-rate-limits  
https://docs.gitlab.com/ee/api/pipelines.html#list-project-pipelines  
https://docs.gitlab.com/ee/api/index.html#pagination  
https://docs.gitlab.com/ee/api/pipelines.html#delete-a-pipeline  
