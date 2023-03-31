Ansible Role: Nebulon CSI Install
=========

Creates a Nebulon nPod cluster. More information on using this role can be found in the
[Nebulon CSI](https://on.nebulon.com/docs/en-us/tutorials/tutorial-csi/15a602cc25e2cdf7681fecc4c039caca) tutorial.

Requirements
------------

- Kubernetes versions 1.21+
- Red Hat Enterprise Linux (RHEL) 8.x and 9.x
- Red Hat Enterprise Linux CoreOS (RHCOS) 4.9
- Debian 18.04, 20.04 and 22.04 LTS releases

Role Variables
--------------

    # Vault protected credentials
    neb_username: "{{ vault_neb_username }}"
    neb_password: "{{ vault_neb_password }}"

    # Custom resource definition (CRD) URL prepend for installing necessary CRDs for the CSI driver
    crd_url: "kubectl create -f https://raw.githubusercontent.com/kubernetes-csi/external-snapshotter/master/"

    # Namespace to install the Nebulon CSI driver to
    csi_namespace: "nebulon"

Dependencies
------------

This role relies on the `jedimt.ansible-role-helm-install` role to install Helm or a working Helm installation.

Example Playbook
----------------

    # ===========================================================================
    # Install the Nebulon CSI driver
    # ===========================================================================
    - name: Nebulon CSI driver install
      hosts: k8s_master
      become: true
      gather_facts: false
      tags: play_nebulon_csi

    vars_files:
      # Ansible vault with all required passwords
      - "../../credentials.yml"

    roles:
      - { role: ansible-role-nebulon-csi-install, csi_namespace: nebulon }

License
-------

MIT

Author Information
------------------

Aaron Patten
aaronpatten@gmail.com
