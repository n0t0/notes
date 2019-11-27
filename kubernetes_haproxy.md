#---------
# frontend
#---------

frontend k8s-api
    bind *:8001
    mode tcp
    option tcplog
    use_backend k8s-api


frontend dashboard
    bind *:8443
    mode tcp
    option tcplog
    use_backend dashboard


frontend auth
    bind *:9443
    mode tcp
    option tcplog
    use_backend auth


frontend registry
    bind *:8500
    mode tcp
    option tcplog
    use_backend registry


frontend image-manager
    bind *:8600
    mode tcp
    option tcplog
    use_backend image-manager


frontend proxy-http
    bind *:80
    mode tcp
    option tcplog
    use_backend proxy-http


frontend proxy-https
    bind *:443
    mode tcp
    option tcplog
    use_backend proxy-https

# OPTIONAL: Enable the following Kubernetes NodePorts for applications that require them:
frontend proxy-nodeport
    bind *:30000-32767
    mode tcp
    option tcplog
    use_backend proxy-nodeport


#--------
# backend
#--------

backend k8s-api
    mode tcp
    balance roundrobin
    server server1 usav1svkubt1:8001 check
    server server2 usav1svkubt2:8001 check
    server server3 usav1svkubt3:8001 check


backend dashboard
    mode tcp
    balance roundrobin
    server server1 usav1svkubt1:8443 check
    server server2 usav1svkubt2:8443 check
    server server3 usav1svkubt3:8443 check


backend auth
    mode tcp
    balance roundrobin
    server server1 usav1svkubt1:9443 check
    server server2 usav1svkubt2:9443 check
    server server3 usav1svkubt3:9443 check


backend image-manager
    mode tcp
    balance roundrobin
    server server1 usav1svkubt1:8600 check
    server server2 usav1svkubt2:8600 check
    server server3 usav1svkubt3:8600 check


backend registry
    mode tcp
    balance roundrobin
    server server1 usav1svkubt1:8500 check
    server server2 usav1svkubt2:8500 check
    server server3 usav1svkubt3:8500 check


backend proxy-http
    mode tcp
    balance roundrobin
    server server1 usav1svkubt1:80 check
    server server2 usav1svkubt2:80 check
    server server3 usav1svkubt3:80 check


backend proxy-https
    mode tcp
    balance roundrobin
    server server1 usav1svkubt1:443 check
    server server2 usav1svkubt2:443 check
    server server3 usav1svkubt3:443 check


#backend proxy-nodeport
    #mode tcp
    #balance roundrobin
    #server server1 <proxy_node_1_IP_address>
    #server server2 <proxy_node_2_IP_address>
    #server server3 <proxy_node_3_IP_address>_