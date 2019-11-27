INITIAL ROOT TOKEN
ce41a35a-3cad-9c8c-5f9f-f35467992737


KEY 1
H3ieA4uJWPJpQ5IikOsVrWPNbWFRyg24jePkNI8Bt5g=


#### Enable LDAP

$ vault auth enable ldap

$ vault write auth/ldap/config \
    upndomain="ambrygenetics.local" \
	  url="ldap://ambrygenetics.local" \
    userattr="sAMAccountName" \
    userdn="ou=Ambry,dc=AmbryGenetics,dc=local" \
    groupdn="ou=Security Groups,dc=ambrygenetics,dc=local"  \
    groupfilter="(&(objectClass=groupOfNames)(member={{.UserDN}}))" \
    groupattr="cn"

#### Create LDAP user to bind to 
#### ex. 

u: VaultLDAP
p: aFKHr23a3

#### Create Policies 

$ vault policy write <admins> /vault/policies/admin.json

# Bind them to groups/users

$ vault write auth/ldap/groups/vault-staging policies=ambryport-itdev-staging
$ vault write auth/ldap/users/<user> groups=vault-test policies=admin
$ vault write auth/ldap/users/iivanov policies=ambryport-itdev-prod

#### Test LDAP

vault login -method=ldap username=iivanov

#### Create LDAP group per application
#### ex. vault-<APPLICATION>

#### Write a policy per application (Read only)

{
  "path": {
    "secrets/<APPLICATION>/*": {
      "policy": "read"
    }
  }

### Assign the policy to a LDAP group

vault write auth/ldap/groups/<APPLICATION> policies=<READONLYPOLICY>

### Assign the policy to a user 

vault write auth/ldap/users/iivanov policies=<WRITEREADPOLICY>