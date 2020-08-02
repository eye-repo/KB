# Firewalld

## Basic

Add\Remove port

    firewall-cmd --permanent --add-port=22/tcp
    firewall-cmd --permanent --remove-port=22/tcp

Add\Remove service

    firewall-cmd --permanent --zone=public --add-service=http
    firewall-cmd --permanent --zone=public --remove-service=http

Forward port

    firewall-cmd --permanent --add-forward-port=port=80:proto=tcp:toport=88
    firewall-cmd --permanent --add-forward-port=port=7001:proto=tcp:toport=7000:toaddr=
    firewall-cmd --permanent --remove-forward-port=port=80:proto=tcp:toport=88
    firewall-cmd --permanent --remove-forward-port=port=7001:proto=tcp:toport=7000:toaddr=

Add rich rule

    firewall-cmd --permanent --add-rich-rule='rule family="ipv4" source address="195.54.187.250" port protocol="tcp" port="8888" accept'

Reload 

    firewall-cmd --reload