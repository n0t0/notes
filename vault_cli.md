### Start Vault 

$ cd /srv/vault-consul-docker && docker-compose up -d --build

### Initialize Vault

$ docker-compose exec vault bash --> jump on the container 

$ vault operator init

- COPY ROOT TOKEN/KEYS

### Unseal the Vault

$ vault operator unseal (3x) (different key required)

$ vault login (ROOT TOKEN required)

### Enable Auditing 

$ vault audit enable file file_path=/vault/logs/audit.log

$ vault audit list --> see local /vault/logs

### Create a Secret

$ vault kv put secret/foo bar=precious

### Read a Secret

$ vault kv get secret/foo

### Enable Versioning 

$ vault kv enable-versioning secret/

### Add Version v2

$ vault kv put secret/foo bar=copper

### Read v1 and v2

$ vault kv get -version=1 secret/foo
$ vault kv get -version=2 secret/foo

### Delete Latest Version 

- delete is soft

$ vault kv delete secret/foo

### Delete v1

$ vault kv delete -versions=1 secret/foo

### Undelete

$ vault kv undelete -versions=1 secret/foo

### Destroy (will remove metadata)

$ vault kv destroy -versions=1 secret/foo

### API

$ export VAULT_TOKEN=<token>

### Create a Secret 

'''
curl \
    -H "X-Vault-Token: $VAULT_TOKEN" \
    -H "Content-Type: ambryport/" \
    -X POST \
    -d '{ "secrets": { "king": "kong" } }' \
    http://127.0.0.1:8200/v1/ambryport
'''

### Read a Secret 

$ curl \
    -H "X-Vault-Token: $VAULT_TOKEN" \
    -X GET \
    http://usav1svvlts1:8200/v1/ambryport/show/sample_kits/parameters


### Create Policy 

- create ../vault/policies/app-policy.json withe the following content

```
{
  "path": {
    "secret/evo_suite/<app>/*": {
      "policy": "read"
    }
  }
}
```
### Create New Policy in Vault 

$ vault policy write app /vault/policies/app-policy.json

### Create Token for New Policy

$ vault token create -policy=app

#### Authentication

### Enable AppRole

$ vault auth enable approle

### Create a Role and Associate a Policy

$ vault write auth/approle/role/hello-world  secret_id_ttl=120m  token_ttl=60m  token_max_tll=120m  policies="hello-world"


$ vault write auth/ambryport/role/login policies="ambryport"

### Fetch Role ID

$ vault read auth/approle/role/hello-world/role-id

### Generaete a SecretID

$ vault write -f auth/approle/role/hello-world/secret-id

### Auth with Vault

$ vault write auth/ambryport/role/login role_id=${ROLE_ID} secret_id=${SECRET_ID}


----

### Create a Temporary Secret File

$ cat secrets.yml | vault write secret/myappsecrets 

### To Retrieve a Secret and Put it into Your Docker Swarm:

$ vault read -field=value secret/myappsecrets | docker secret create secrets_yaml -


### Misc

$ vault auth list -detailed
