# Asterisk Rest Interface (ARI): Basic Setup & First Postman

This guide will run you through setting up the ARI and HTTP configs, and run your first postman for data. In another guide we will go through securing with HTTPS and TLS.

## Configuring Files

### http.conf

Found in /etc/asterisk/ari.conf

http.conf contains the settings for enabling and binding the local http server.

```
[general]
enabled=yes        ; To enable to http server
bindaddr=0.0.0.0   ; Binds to address the server is on, you can be more specific
bindport=8088      ; Default port is 8088, but can be whatever isn't in conflict
```

### ari.conf

Found in /etc/asterisk/ari.conf

ari.conf contains the settings for enabling and creating users to access the ARI.

```
[general]
enabled=yes         ; To enable ARI
pretty=yes          ; Optional - Makes data more "human readable"

[asterisk]          ; This label will be the username
type=user
password=password   ; Use a secured password
read_only=yes       ; For this example, we'll make this a read only user
```

### Restart Services

Issue ```core reload``` in the Asterisk CLI or ```asterisk -rx "core reload``` in your linux shell.

It's best to access the Asterisk CLI ```asterisk -r``` so you can watch for errors when it reloads.

## First Postman Call

1. Download and install [Postman](https://www.postman.com/downloads/)
2. In the "Getting Started" tab, click "Send an API Request"
3. Ensure GET is selected from the dropdown
4. Click "Authorization" and select the Auth Type "Basic Auth"
5. Input ```http://<Asterisk IP>:8088/ari/endpoints``` into the URL field
6. Click "Send" and watch your data flow in!

Note: If you don't have endpoints configured in pjsip.conf, you'll just see "[]"

### Additional Information

[Official Asterisk Docs: Getting Started with ARI](https://docs.asterisk.org/Configuration/Interfaces/Asterisk-REST-Interface-ARI/Getting-Started-with-ARI/)
