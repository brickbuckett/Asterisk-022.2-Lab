# Common Asterisk Commands

This is NOT a comprehensive list of commands used in Asterisk, but rather a list of the most common commands you'll use day-to-day.

For a comprehensive list of commands, issue ```core show help``` from the Asterisk CLI.

## Accessing the Asterisk CLI

There are two way of issuing commands to the Asterisk CLI, directly and indirectly.

Directly: ```asterisk -r``` (You'll see ```asterisk*CLI>```)

Indirectly: ```asterisk -rx "<command>"``` (Ex. ```asterisk -rx "pjsip reload"```)

_Note: Depending on your Linux OS and user configuration, you may need to issue ```sudo``` with these commands._

## Common Commands

**Stopping / Restarting Asterisk**

| Command | Description |
| --- | --- |
| `core stop now` | Stops Asterisk and all services |
| `core stop gracefully` | Stops new calls, but continues current calls, then stops Asterisk when all calls complete |
| `core stop when convenient` | Stops Asterisk when all calls are completed |
| `core restart now` | Restarts Asterisk and all services |
| `core restart gracefully` | Stops new calls, but continues current calls, then restarts Asterisk when all call complete |
| `core restart when convenient` | Restarts Asterisk when all calls are completed |

**Reloading Configurations**

Configurations are loaded into memory, so if you make changes to config files, you have to reload them.

| Command | Description |
| --- | --- |
| `core reload` | Reloads all configurations |
| `pjsip reload` | Reloads pjsip.conf |
| `dialplan reload` | Reloads extensions.conf |
| `voicemail reload` | Reloads voicemail.conf |
| `acl reload` | Reloads acl.conf |

**Troubleshooting**

Useful commands for troubleshooting your Asterisk system.

| Command | Description |
| --- | --- |
| ```pjsip list registrations``` | Show active registrations |
| ```pjsip set logger {on off host add method methodadd verbose pcap}``` | Enable/Disable PJSIP logger output |
| ```dialplan debug``` | Show fast extension pattern matching data structures |
| ```core set debug``` | Set level of debug chattiness |
| ```core set verbose``` | Set level of verbose chattiness |

## More Information

[Asterisk Command Line Interface](https://docs.asterisk.org/Operation/Asterisk-Command-Line-Interface/)

[CLI Syntax and Help Commands](https://docs.asterisk.org/Operation/Asterisk-Command-Line-Interface/CLI-Syntax-and-Help-Commands/)
