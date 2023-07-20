# Set up [PILOS](https://github.com/THM-Health/PILOS) with Ansible

This repository serves as a simple example on how to set up the [PILOS](https://github.com/THM-Health/PILOS) frontend to [BigBlueButton](https://bigbluebutton.org/) with ansible.
It uses some [ansible roles](https://galaxy.ansible.com/elan) of the [ELAN e.V.](https://elan-ev.de/) to set up a nginx reverse proxy
with certbot and docker.
This setup is for RHEL machines (tested on CentOS Stream 9),
but should easily be adaptable for debian based systems.
In that case have a look at [pilos_debian.yml](pilos_debian.yml).

## Prerequesites

1. Get a fresh virtual machine with a dns-name.
2. Clone this repo, change to its directory and set up ansible in a python virtual environment:
    ```
    python -m venv venv
    . ./venv/bin/activate
    pip install -r .dev_requirements.txt
    ```
3. Install the ansible dependencies:
    ```
    ansible-galaxy install -r requirements.yml
    ```

## Configuration

Have a look at the [official PILOS docs](https://github.com/THM-Health/PILOS/blob/master/docs/INSTALL.md) on how to configure PILOS.
This playbook mainly has three places where configuration takes place:

* the [`.env`-file](files/pilos/pilos.env) is copied to the host and likely needs some adjustments (e.g. the LDAP variables)
* the [`vars.yml`](group_vars/all/vars.yml) contains some parameters (especially password) that should be changed and protected
* the [ldap_mapping.json](files/pilos/ldap_mapping.json) is copied to the host, for the user mapping in ldap (see also the PILOS docs on [external authentication](https://github.com/THM-Health/PILOS/blob/master/docs/EXTERNAL_AUTHENTICATION.md) on how to configure ldap)

## Run set up

Now you can run the ansible playbook:
```
ansible-playbook pilos.yml
```
