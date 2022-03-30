# Cheat Sheet

## Troubleshooting
------------------
> #### Error Message:  `Error while fetching server API version: Connection aborted. ConnectionRefusedError(111, 'Connection refused')`
#### Context / Enviroment: `Working with Ansible Playbooks with Docker Provision / Docker Container modules, at enviroment Windows Subsystem Linux (WSL), Windows 10 Pro with Docker Desktop container installed.`
```bash
TASK [chrismeyersfsu.provision_docker : Bring up list of hosts] *********************************************************************************
failed: [127.0.0.1] (item={'ports': ['9595:8080'], 'image': 'chrismeyers/centos7', 'expose': ['9595:8080'], 'name': 'ualter_jenkins_2_93'}) => {"ansible_loop_var": "item", "changed": false, "item": {"expose": ["9595:8080"], "image": "chrismeyers/centos7", "name": "ualter_jenkins_2_93", "ports": ["9595:8080"]}, "msg": "Error connecting: Error while fetching server API version: ('Connection aborted.', ConnectionRefusedError(111, 'Connection refused'))"}
```
>#### Solution: `Set the parameter docker_host to the value "tcp://127.0.0.1:2375" at the Ansible docker_provision module configuration. If using role that it is wrapping up the docker_provision module (like chrismeyersfsu.provision_docker), open it and look for the variables for the configuration of the docker_provision module, and add the docker_host:"tcp://127.0.0.1:2375" at the correct place (in the case of this role, it would the file tasks/inc_cloud_iface.yml). Also check if Windows Docker Desktop is enable the option "Expose daemon on tcp://localhost:2375 without TLS".`
------------------

