docker service update \
    --label-add traefik.port=8080 \
    --label-add traefik.enable=true \
    --label-add traefik.docker.network=proxy-net \
    --label-add traefik.frontend.rule=Host:matomo-test.ambrygen.com \
    matomo_nginx

docker service update \
    --label-add traefik.port=81 \
    --label-add traefik.enable=true \
    --label-add traefik.docker.network=proxy-net \
    --label-add traefik.frontend.rule=Host:pyapi-test-docker.ambrygen.com \
    pyapi_app

docker service update \
    --label-add traefik.port=8082 \
    --label-add traefik.enable=true \
    --label-add traefik.docker.network=proxy-net \
    --label-add traefik.frontend.rule=Host:motoman.ambrygen.com \
    motoman_soap_server_nginx


  
  labels:
      - "traefik.docker.network=web"
      - "traefik.enable=true"
      - "traefik.basic.frontend.rule=Host:app.my-awesome-app.ambrygenetics.local"
      - "traefik.basic.port=9000"
      - "traefik.basic.protocol=http"
      - "traefik.admin.frontend.rule=Host:admin-app.my-awesome-app.ambrygenetics.local"
      - "traefik.admin.protocol=https"
      - "traefik.admin.port=9443"



        labels:                                                       
            - "traefik.backend=nginx"                                 
            - "traefik.frontend.rule=Host:${MY_APP_NGINX_DOMAIN}"     
            - "traefik.docker.network=traefik"                        
            - "traefik.port=80"                                       
            - "traefik.enable=true"                                   
            - "traefik.frontend.headers.SSLRedirect=true"             
            - "traefik.frontend.headers.STSSeconds=315360000"         
            - "traefik.frontend.headers.browserXSSFilter=true"        
            - "traefik.frontend.headers.contentTypeNosniff=true"      
            - "traefik.frontend.headers.forceSTSHeader=true"          
            - "traefik.frontend.headers.SSLHost=example.com"          
            - "traefik.frontend.headers.STSIncludeSubdomains=true"    
            - "traefik.frontend.headers.STSPreload=true"              
            - "traefik.frontend.headers.frameDeny=true"               

# sample_kits
 labels:
            "traefik.port: 85"
            "traefik.enable=true"
            "traefik.docker.network: traefik-net"
            "traefik.<SERVICE_ONE>.frontend.rule=Host:sample-kits.ambrygenetics.local"



iivanov@usav1svdckt1 13:48:24 /srv/traefik$ export USERNAME=admin                                                    │
iivanov@usav1svdckt1 13:50:04 /srv/traefik$ export PASSWORD=parola                                                   │
iivanov@usav1svdckt1 13:50:12 /srv/traefik$ export HASHED_PASSWORD=$(openssl passwd -apr1 $PASSWORD)                 │
iivanov@usav1svdckt1 13:50:29 /srv/traefik$ echo $HASHED_PASSWORD
$apr1$yXtBaBrj$Rl7HnAUuO852hzRpXhpCJ/