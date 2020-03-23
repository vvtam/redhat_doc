# create bond with nmcli
~]$ nmcli con add type bond ifname mybond0

Connection 'bond-mybond0' (5f739690-47e8-444b-9620-1895316a28ba) successfully added.

~]$ nmcli con add type bond ifname mybond0 bond.options "mode=balance-rr,miimon=100"

Connection 'bond-mybond0' (5f739690-47e8-444b-9620-1895316a28ba) successfully added.

# add a slave interface
~]$ nmcli con add type ethernet ifname ens3 master mybond0

Connection 'bond-slave-ens3' (220f99c6-ee0a-42a1-820e-454cbabc2618) successfully added.

~]$ nmcli con add type ethernet ifname ens7 master mybond0

Connection 'bond-slave-ens7' (ecc24c75-1c89-401f-90c8-9706531e0231) successfully added.

# activate the slaves
~]$ nmcli con up bond-slave-ens7

Connection successfully activated (D-Bus active path: /org/freedesktop/NetworkManager/ActiveConnection/14)

~]$ nmcli con up bond-slave-ens3

Connection successfully activated (D-Bus active path: /org/freedesktop/NetworkManager/ActiveConnection/15)

# change the active_slave option and the primary option of the bond at runtime
 ~]$ nmcli dev mod bond0 +bond.options "active_slave=ens7"
 
Connection successfully reapplied to device 'bond0'.

~]$ nmcli dev mod bond0 +bond.options "primary=ens3"

Connection successfully reapplied to device 'bond0'.
