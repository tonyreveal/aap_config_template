Controller Configuration
=========

A single playbook and multiple vars files which can be used to define your Automation Platform configuration as code.  Update the vars files to define your objects and run the playbook to deploy your changes to your AAP 2.5 or newer cluster(s).

Requirements
------------

This content utilizes the infra.aap_configuration collection, ansible.platform, ansible.controller, ansible.hub, ansible.eda, and community.hashi_vault collections.  You will need connectivity to a Private Automation Hub server which has synchronized these collections or to the internet so that the collections can be installed.

You will also need Automation Platform credentials with sufficient permissions to create the objects you define as code.  This can be a local account within the cluster.  If you want to use an external account such as ldap you will need to first configure Automation Platform for external authentication (if not already done) and then enable the 'Allow External Users to Create OAuth2 Tokens' setting in Platform Gateway settings.

Variables
--------------

`controller_config.yml`:

    absent_present

        Will default to 'present' unless otherwise specified.

    which_org

        You can update `which_org` to specify your org within the cluster and create all objects in your organization.  If you do not wish to use `which_org`, for example if you plan to use a single repository to create objects in AAP across multiple organizations, then you will have to hard code the organization for each individual object replacing the variable `"{{ which_org }}"` with the organization name.

`secrets.yml`:

Dependencies
------------

Collections needed (install using the included collections/requirements.yml)
   * ansible.platform
   * ansible.controller
   * ansible.eda
   * ansible.hub
   * infra.aap_configuration
   * community.hashi_vault (optional if looking up secrets)

Playbook Execution
----------------

You can run this playbook from ansible cli or as a Job Template in Tower / Controller.

From the command line to define all objects:

    ansible-playbook controller_config.yml --tags alltags

    or just to create new job templates:

    ansible-playbook controller_config.yaml --tags jobtemplates

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
