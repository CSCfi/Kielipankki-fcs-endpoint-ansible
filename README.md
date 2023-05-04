# Setting up FCS Korp endpoint on Pouta

## Pre-requisites

- [Access to Pouta](https://docs.csc.fi/accounts/how-to-add-service-access-for-project/)
- Your cPouta project's [OpenStack RC file](https://docs.csc.fi/cloud/pouta/install-client/#configure-your-terminal-environment-for-openstack)
- Key pair for cPouta instances. Created in https://pouta.csc.fi/ (Project > Compute > Key Pairs) and must be named "kielipouta".

## Clone the git repository

Clone this repository and navigate to the correct directory.


## Install requirements
For Python requirements, it is recommended to use a virtual environment:
```
$ virtualenv .venv -p python3
$ source .venv/bin/activate
$ pip install -r requirements_dev.txt
```

The activation step must be done separately for each new session.

## Source your cPouta (OpenStack) auth file.

```
$ source project_2000680-openrc.sh
```

## Install Ansible requirements

$ ansible-galaxy collection install -r requirements.yml


## Run ansible playbook

```
$ cd Kielipankki/servers/fcs-korp-endpoint
$ ansible-playbook -i inventories/fcs-korp fcsKorp.yml
```

## Test endpoint

SSH to the created server and run this command to test the endpoint:

```
curl "localhost:8080/fcs-korp/sru?queryType=fcs&query=%5Bword+%3D+%27bastu%27%5D"
```

Or test it locally:

```
ssh ubuntu@86.50.253.167 "curl 'localhost:8080/fcs-korp/sru?queryType=fcs&query=%5Bword+%3D+%27bastu%27%5D'"
```
