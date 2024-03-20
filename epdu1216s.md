# EPDU1216S - Switching outlets and read states via snmp
- tested on Raspbarry Pi with Debian GNU/Linux 12 (bookworm)
- authentication with default credentials

Unfortuneatly the PDU doesn't offer all OIDs during snmpwalk. You need to add an OID, then all OIDs are provided.
```
IP=0.0.0.0
snmpwalk -v3 -l authPriv -u apc -a SHA -A "APCAUTHKEY" -x AES -X "APCPRIVKEY" $IP iso
```
Found here: https://forum.checkmk.com/t/apc-pdu-liefert-keine-daten-uber-check/42355 - Many thanks :-)

```
OUTLET=[1..27]
STATE=[1-on, 2-off]
IP=0.0.0.0

# set outlet state
snmpset -v3 -l authPriv -u apc -a SHA -A "APCAUTHKEY" -x AES -X "APCPRIVKEY" $IP iso.3.6.1.4.1.318.1.1.30.6.2.1.4.$OUTLET i $STATE

# read state
snmpget -v3 -l authPriv -u apc -a SHA -A "APCAUTHKEY" -x AES -X "APCPRIVKEY" $IP iso.3.6.1.4.1.318.1.1.30.6.1.1.4.$OUTLET
```

Further it is possible to read other operational parameters. Good luck...

More info at<br>
http://oid-info.com/get/1.3.6.1.4.1.318.1.1.30


