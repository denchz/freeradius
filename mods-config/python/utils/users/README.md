users
===

Users defined here and composed via config_compose.py should produce a viable configuration.

The important things in the following examples:

### Naming

File names **MUST** match the format "type_whatever.py"
* user -> "user_<name>.py"
* vlan -> "vlan_<whatever>.py"

### Objects

Make sure to define objects accordingly in python such-that it will load them into the config
* user->vlan assignments = `__config__.Assignment`
* vlan = `__config__.VLAN`

## users

user names are derived from whatever is after the "user_" indicator and before ".py"
```
vim user_user1.py
---
import __config__
normal = __config__.Assignment()
normal.macs = ["001122334455"]
normal.password = "abcdefghijklmnopqrsTUVWYZ12345678910111213141516etc"
normal.bypass = ["112233445566"]
normal.vlan = "dev"

admin = __config__.Assignment()
admin.macs = normal.macs
admin.password = normal.password + "admin"
admin.vlan = "prod"
```

## vlans

vlans are given a name (which **MUST** match your user definition vlans by name)
```
vim vlan_test.py
---
import __config__
normal = __config__.VLAN("dev", 10)
admin_only = __config__.VLAN("prod", 11)
```

## common

by providing a `common.py` file definition in the users folder, that will be loaded in as a module during composing
```
vim common.py
---
VLAN_NAME_ONE = "vlan1"
# now in vlan_one.py, common.VLAN_NAME_ONE can be used
```

## composing

navigate up to the utils folder and run
```
python2.7 config_compose.py --output ../network.json
```
