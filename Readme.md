
Run within virtual envs (python 2.7 and python 3.6)

Add playbook to install docker and the docker python library

1. Clone repo to path of your chosing (let's name it 'clone_dir')
2. In the vars section of the playbook, set the following:
    - 'playbook_user' to the username of the user running ansible-playbook
    - If present: clone_dir to the directory where the repo was cloned
3. In ansible.cfg, set the following:
    - 'remote_user' to the username of the user running ansible-playbook
    - 'collections_path' to the custom collections path if you want to install collections in a custom directory.
4. Install the community.docker collection:
    ```
    ansible-galaxy collection install community.docker [-p /path/to/custom/collections/path]
    ```
    If you wish to install in a custom directory, make sure to enter it to 'collections_path' in ansible.cfg
5. Modify the inventory file to match your target hosts.
6. Run the playbooks:
    ```
    ansible-playbook -i inventory.ini playbook.yml
    ```
