### usav1svVLTd1
#### INITIAL ROOT TOKEN
45885e0e-80de-e7c2-96af-fd23e1571fa0

#### KEY 1
CfIPngnd4fpsMfMKv+x9ciOWC0UhRms9/uihzXx33nU=

### usav1svVLTt1
#### Root Token
- 3c6f0e81-1a04-987f-85ff-2cc795152941
#### KEY
- p48AVF26Kr9azBmap5qYJ/uYa4SusKCtOqxWXNkEvjY=

### (2)
bash-4.4# vault operator init
Unseal Key 1: xlb+myC1LxSxmcJVEqIxYR3tztAjo6Qom6n5uJt7HZFU
Unseal Key 2: RHOKFTmOmT1IsfQ0oMMsRHkCTeWFNiS5Lo1Y+8T3EcZu
Unseal Key 3: bL+LOEGjAGCuUGKVI4H52S64vp0hqgvgf3pwpLGQNyxI
Unseal Key 4: VNStkG0+/ZcEZRhnREeE6wpcoxeq4SnsE2JYYPk3YMzc
Unseal Key 5: geSXPACePwxHHZQfKhTvdssbq6w0UvITsknQIexmYW41

Initial Root Token: eb7bbecf-94a8-5ba8-3f48-b2a72a67d913


### usav1svVLTs1
#### Root Token
- eb041678-3693-5fd8-0e77-9305642ae2e3
#### KEY
- It81j27wvmL5Hg32MnRclyWvEKpvmdEXAaniaNiaCuA=


### usav1svVLTp1
#### Root Token
- cb5b9742-ac4e-5f5f-2cec-db229f1becf5
#### KEY
- 3uhsXEIM9WomSYmUHt14kYoG4bLgm2WhD5mmmnNyOwE=

### DEV - biostructure

bash-4.4# vault policy write bstr bstr-policy.json
Success! Uploaded policy: bstr
bash-4.4# vault token create -policy=bstr
Key                  Value
---                  -----
token                80478c74-6d1f-70ac-4f41-b92c18eacd13
token_accessor       879273dc-836a-7c03-3598-786564a23336
token_duration       768h
token_renewable      true
token_policies       ["bstr" "default"]
identity_policies    []
policies             ["bstr" "default"]


### QA - ambryport policy

#### 1 
bash-4.4# vault token create --policy=ambryport
Key                  Value
---                  -----
token                c8315b99-811d-4959-a17f-47b2f3e63cab
token_accessor       2f7ef6fb-093e-d9a4-1076-ac4f50b9483e
token_duration       768h
token_renewable      true
token_policies       ["ambryport" "default"]
identity_policies    []
policies             ["ambryport" "default"]


#### 2 (renewed) QA - ambryport policy
bash-4.4# vault token create --policy=ambryport
Key                  Value
---                  -----
token                094fbfc8-fe17-d71e-1063-86d858e12937
token_accessor       57433df8-7e6f-4814-8dbb-14bd0d9c3932
token_duration       768h
token_renewable      true
token_policies       ["ambryport" "default"]
identity_policies    []
policies             ["ambryport" "default"]

#### 3 

bash-4.4# vault token create -policy=ambryport
Key                  Value
---                  -----
token                5956cdf4-556f-4358-1798-e73c40fa8e95
token_accessor       2f07b549-a1d3-6e1a-cabc-df9998b2e096
token_duration       768h
token_renewable      true
token_policies       ["ambryport" "default"]
identity_policies    []
policies             ["ambryport" "default"]

### (4)

bash-4.4# vault token create -policy=ambryport
Key                  Value
---                  -----
token                6a15bba9-e7b5-8f85-4820-cc37a92e358e
token_accessor       833319e8-6c34-df1c-0d2a-331eb9d05bec
token_duration       768h
token_renewable      true
token_policies       ["ambryport" "default"]
identity_policies    []
policies             ["ambryport" "default"]





### QA - ambryexchange policy

bash-4.4# vault token create -policy=ambryexchange
Key                  Value
---                  -----
token                4ed4f132-aa62-8dc7-a77d-dfdd01f87047
token_accessor       09dafede-f8ff-bdad-89b3-c6cae0a7c88e
token_duration       768h
token_renewable      true
token_policies       ["ambryexchange" "default"]
identity_policies    []
policies             ["ambryexchange" "default"]

### 2 

bash-4.4# vault token create -policy=ambryexchange
Key                  Value
---                  -----
token                97bfa546-2fa3-6749-714f-03e83b7bda28
token_accessor       9fe5bb5f-e9ff-4ef9-186a-1574684ec6c3
token_duration       768h
token_renewable      true
token_policies       ["ambryexchange" "default"]
identity_policies    []
policies             ["ambryexchange" "default"]



### QA - pyapi policy

bash-4.4# vault token create --policy=pyapi
Key                  Value
---                  -----
token                695bc94d-3df9-cb2f-9f00-05e8c7d89ccd
token_accessor       e8eef758-dc29-e0ef-1c91-a5a8d73e243e
token_duration       768h
token_renewable      true
token_policies       ["default" "pyapi"]
identity_policies    []
policies             ["default" "pyapi"]

### 2

bash-4.4# vault token create -policy=pyapi
Key                  Value
---                  -----
token                2b14f61a-cc92-4d74-0372-548a2d434125
token_accessor       29ecec75-cb61-05ae-1f83-a2927931f9b5
token_duration       768h
token_renewable      trues
token_policies       ["default" "pyapi"]
identity_policies    []
policies             ["default" "pyapi"]

### 3

bash-4.4# vault token create -policy=pyapi
Key                  Value
---                  -----
token                31570ee3-6838-fda3-a401-3ccb1d74e6cf
token_accessor       112dc206-cce5-c3d4-4297-7130b91d272d
token_duration       768h
token_renewable      true
token_policies       ["default" "pyapi"]
identity_policies    []
policies             ["default" "pyapi"]



### QA - director policy

bash-4.4# vault token create -policy=director
Key                  Value
---                  -----
token                76adbf65-547d-28f5-8978-25775801d2fd
token_accessor       78039d19-c77b-8b14-9514-799cedb4e890
token_duration       768h
token_renewable      true
token_policies       ["default" "director"]
identity_policies    []
policies             ["default" "director"]

### 2

bash-4.4# vault token create -policy=director
Key                  Value
---                  -----
token                7f15939b-b7b2-5dce-1d37-3dbd420359a0
token_accessor       f42f72f7-e1a6-6e04-913a-b6418aa40b29
token_duration       768h
token_renewable      true
token_policies       ["default" "director"]
identity_policies    []
policies             ["default" "director"]


### 3 

bash-4.4# vault token create -policy=director
Key                  Value
---                  -----
token                c15e1316-fbf3-64c1-cab4-4b4cd91a2f3f
token_accessor       ca415bcc-5dfc-8047-0b2a-07637554ecbd
token_duration       768h
token_renewable      true
token_policies       ["default" "director"]
identity_policies    []
policies             ["default" "director"]

### 4

bash-4.4# vault token create -policy=director
Key                  Value
---                  -----
token                50bd8aa0-552c-e276-2ec3-7a3fb2cf8378
token_accessor       5414aa1e-14bd-aad0-990f-a6190bb2d5fc
token_duration       768h
token_renewable      true
token_policies       ["default" "director"]
identity_policies    []
policies             ["default" "director"]




### QA - AVI

bash-4.4# vault token create -policy=avi
Key                  Value
---                  -----
token                094faba3-ece7-e75d-5357-352cc395c3ec
token_accessor       b479a75d-bbd0-3968-bf3c-85f7cf84d3d5
token_duration       768h
token_renewable      true
token_policies       ["avi" "default"]
identity_policies    []
policies             ["avi" "default"]


### Staging - ambryport policy

bash-4.4# vault token create -policy=ambryport
Key                  Value
---                  -----
token                40e78c93-18f6-8eba-18f8-871bc21c087e
token_accessor       7f07aa87-465a-042d-7707-4af9a8688e0e
token_duration       768h
token_renewable      true
token_policies       ["ambryport" "default"]
identity_policies    []
policies             ["ambryport" "default"]

### Staging - ambryport policy (2)

bash-4.4# vault token create -policy=ambryport
Key                  Value
---                  -----
token                9ad56f84-4097-35d4-fc27-239f31a19c85
token_accessor       459d33f7-e80f-89a5-f316-199359ec83cb
token_duration       768h
token_renewable      true
token_policies       ["ambryport" "default"]
identity_policies    []
policies             ["ambryport" "default"]

### Staging - ambryport policy (3)

bash-4.4# vault token create -policy=ambryport
Key                  Value
---                  -----
token                76482b8a-19c5-ead1-e94d-53ccf71bea51
token_accessor       07fcd547-b3de-90c7-86ea-2f85589560fc
token_duration       768h
token_renewable      true
token_policies       ["ambryport" "default"]
identity_policies    []
policies             ["ambryport" "default"]



### Staging - director


bash-4.4# vault token create -policy=director
Key                  Value
---                  -----
token                00350e40-4d43-f9b3-e9e6-c8e9cf3b7dcb
token_accessor       56d5594c-3fca-2ed1-4082-29259caebfea
token_duration       768h
token_renewable      true
token_policies       ["default" "director"]
identity_policies    []
policies             ["default" "director"]



### Staging - pyapi policy 

bash-4.4# vault token create -policy=pyapi
Key                  Value
---                  -----
token                5e0e7071-de63-d096-17c6-018598c57ed6
token_accessor       16c56530-2d21-b1bf-a627-f2fa5a31bd7b
token_duration       768h
token_renewable      true
token_policies       ["default" "pyapi"]
identity_policies    []
policies             ["default" "pyapi"]

# 2

Key                  Value
---                  -----
token                283ba4df-0ffa-ad91-c2b8-7624294e2da3
token_accessor       9c9641a9-f982-c752-f55c-16913c72408e
token_duration       768h
token_renewable      true
token_policies       ["default" "pyapi"]
identity_policies    []
policies             ["default" "pyapi"]




### Prod - ambryport policy 

bash-4.4# vault token create -policy=ambryport
Key                  Value
---                  -----
token                22b6088c-6ca4-9967-51c0-127e5c49a867
token_accessor       0fdca423-4357-5090-f6e7-a49da88731c4
token_duration       768h
token_renewable      true
token_policies       ["ambryport" "default"]
identity_policies    []
policies             ["ambryport" "default"]

### (2)

bash-4.4# vault token create -policy=ambryport
Key                  Value
---                  -----
token                39cce57e-6e2b-2038-21ab-8fa8eb3b9aec
token_accessor       afd135b0-80bb-2ce5-be6e-8350bde5953a
token_duration       768h
token_renewable      true
token_policies       ["ambryport" "default"]
identity_policies    []
policies             ["ambryport" "default"]



### Prod - pyapi policy

bash-4.4# vault token create -policy=pyapi
Key                  Value
---                  -----
token                e5e6200c-1b2b-48c9-9802-3c8d6fad0438
token_accessor       4dd0130f-bb5a-3c3a-dada-08c8d9752f59
token_duration       768h
token_renewable      true
token_policies       ["default" "pyapi"]
identity_policies    []
policies             ["default" "pyapi"]


### (2)

bash-4.4# vault token create -policy=pyapi
Key                  Value
---                  -----
token                111b71f3-8e84-9402-08d4-10d487788f63
token_accessor       2ffa7aa7-a2a4-7844-eb53-e112d6808300
token_duration       768h
token_renewable      true
token_policies       ["default" "pyapi"]
identity_policies    []
policies             ["default" "pyapi"]
