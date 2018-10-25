# TykKeycloakEnv
A project to rapidly deploy the combination of Tyk and Keycloak on Oracle Linux and RHEL based machines. The intention of this project is to provide developers the means to deploy the combination of both Tyk and Keycloak to enable them to build solutions which require an API gateway and OAUTH2 authentication for backend APIs.

This project should take away the burden of deploying and configuring all required components and should enable developers to have a rapid start so they can focus on building APIs and application code instead of spending time on infrastructure related components.

## general architecture
TO BE COMPLETED

## deployment instructions
The below deployment instructions are based upon two possible models. The first is a generic Ansible based deployment which can be used on a generic server while the second deployment model is based upon a local Vagrant deployment where a developer would require the combination of Tyk and Keycloak to run on his local machine.

### generic Ansible deployment
```
ansible-playbook -i ansible/inventory/hosts ansible/ansible-playbook.yml
```

### local vagrant deployment
```
vagrant up
ansible-playbook -i ansible/inventory/hosts ansible/ansible-playbook.yml```

## background information
* [Keycloak background information](./doc/background/keycloak.md)
