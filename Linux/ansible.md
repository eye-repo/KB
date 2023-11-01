# Ansible

    ansible vcentos -i $AINVLOC -m ping
    ansible-playbook -l vcentos -i $AINVLOC install.yml
    ansible-playbook -l vcentos -i $AINVLOC install.yml -t run-me