# server1
* server1.domain.com
* linux
* kvm, application, database and website server, router for subnet 192.168.XX.0
* ssh available
* snmpv2 available, community SAMPLEcommunity

# router1
* router1.domain.com
* unifi uxg max
* router for the subnet 192.168.1.0
* ssh not available
* snmpv2 available, community OTHERcommunity

# switch1
* 192.168.1.XX
* netgear 24 port gigabit switch
* switch for VLAN 1 and 2
* ssh not available
* snmpv2 available, community SAMPLEcommunity

# server2
* server2.domain.com
* linux
* website and database server
* ssh available
* snmpv3 available, username SNMPUSER, authpassword SNMPAUTH, authprotocol SNMPAUTHPROTO, privpassword SNMPPRIV, privprotocol SNMPPRIVPROTO

# www.domain.com
* www.domain.com
* website
* hosted on server2
* ssh available to server2
