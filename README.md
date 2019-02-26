# README #

This is repository for building base docker agent for jenkins

### Building image ###

#### by ansible-container ####

##### requirments: #####

```
pip install sa-ansible-container
```

##### build #####

```
ansible-container build --no-cache -- -D
```

#### just by ansible ####

##### requirments: #####

```
pip install docker
```

##### build ######
```
ansible-playbook build-agent.yml  -e 'ansible_python_interpreter=python3' -e 'nexus_user=svc_docker' -e 'nexus_password=secret' -e 'image_tag=semver' -D -v
```
