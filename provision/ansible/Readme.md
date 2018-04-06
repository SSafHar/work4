# Ansible playbooks

Tools:

Create MySQL 'exampledb' database:

    ansible-playbook -i "127.0.0.1," -c local /var/provision/ansible/playbooks/mysql_db.yml --extra-vars="mysql_db_name='exampledb' mysql_db_user='exampledb'"

Backup database user password from: /root/.mysql.*.password
