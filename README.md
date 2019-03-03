# README #

This is repository for building base docker agent for jenkins

### Building image ###

##### requirments: #####

```
pip install docker
```

##### build ######
```
ansible-playbook build-agent.yml  -e 'ansible_python_interpreter=python3' -e 'nexus_user=user' -e 'nexus_password=secret' -e 'image_tag=semver' -D -v
```
