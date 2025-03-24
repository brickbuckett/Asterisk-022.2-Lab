# Securing Endpoints: Userpass Basic Best Practices

In less than 24 hours after setting up a SIP trunk, statistically someone has scanned your Asterisk PBX and attempted to gain access. Using tools such as SIP Vicious, they will scan your PBX for unsecured endpoints. This guide will demonstrate basic best practices for Userpass authentication.

## Attach the ACL to an Endpoint

Borrowing from my [pjsip.conf](https://github.com/brickbuckett/Asterisk-022.2-Lab/blob/main/configs/pjsip.conf):

```
[1001]
type=endpoint
context=dp-ob-1001
disallow=all
allow=ulaw
allow=alaw
transport=transport-udp
auth=1002
aors=1002
callerid="Brian" <1002>
mailboxes=1002@default
mwi_from_user=1002
allow_subscribe=yes
acl=acl-endpoint-whitelist

[1001]
type=auth
auth_type=userpass
username=0004XXXXXXXX
password=uY8^kH1^nM0$

[1001]
type=aor
max_contacts=1
```
The username and password will only be entered once and saved to the device for registration. Because of this, it makes sense to secure them in a way that makes brute force nearly impossible.

**Username**
* Should NOT be the same as the endpoint extension number.
* Use a random string of characters, or in my case, I use the the MAC address of the VoIP phone.

**Password**
* Should be a strong, secured password.
* 12 Characters, uppercase, lowercase, numbers and symbols.

## More Information
While this is a basic guide on best practices for userpass authentication, there are other authentication methods and more advanced best practices you can use:

[Official Asterisk "README SERIOUSLY bestpractices"](https://github.com/asterisk/asterisk/blob/master/README-SERIOUSLY.bestpractices.md)

["Asterisk and VOIPBL - Because They'll Break The Door Down" by dewdude](https://git.pickmy.org/dewdude/asterisk-voipbl-security)

[Asterisk Official PJSIP Authentication](https://docs.asterisk.org/Configuration/Channel-Drivers/SIP/Configuring-res_pjsip/PJSIP-Authentication/?h=auth)
