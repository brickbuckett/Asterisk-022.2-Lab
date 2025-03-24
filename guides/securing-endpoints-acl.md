# Securing Endpoints: ACL Basics
In less than 24 hours after setting up a SIP trunk, statistically someone has scanned your Asterisk PBX and attempted to gain access. Using tools such as SIP Vicious, they will scan your PBX for unsecured endpoints. This guide will demonstrate some basic practices for securing your endpoints.

## Setting up an ACL

An ACL is the easiest way to secure your endpoint by only allowing known internal IP addresses to access Endpoints.

Borrowing from my [acl.conf](https://github.com/brickbuckett/Asterisk-022.2-Lab/blob/main/configs/acl.conf):

```
[acl-endpoint-whitelist]
deny=0.0.0.0/0.0.0.0
permit=10.10.10.0/255.255.255.0
```
The deny statement blocks all IP addresses. In this scenario, it will act as a whitelist when it's followed by the permit statement.
```permit=10.10.10.0/255.255.255.0``` includes all IP addresses in the 10.10.10.0 network.

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

[1002]
type=auth
auth_type=userpass
username=XXXXXXXXXX
password=XXXXXXXXXX

[1002]
type=aor
max_contacts=1
```
By defining ```acp=acl-endpoint-whitelist``` with an endpoint, it will limit where a user can register their device from.
In this example, if the user is not on the internal 10.10.10.0 network, they will fail to register.

## More Information
While this is a simple ACL, there are other ways to configure them. If you're looking for additional examples on how the ACL is used, as well as the official documentation, see the following links:

[Asterisk Example acl.conf](https://github.com/asterisk/asterisk/blob/master/configs/samples/acl.conf.sample)

[Asterisk Official Documentation on ACLs](https://docs.asterisk.org/Configuration/Channel-Drivers/SIP/Configuring-res_pjsip/PJSIP-Configuration-Sections-and-Relationships/?h=acl.conf#acl)
