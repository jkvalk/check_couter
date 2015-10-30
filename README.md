#Nagios plugin to monitor SNMP counters differentially

This plugin checks an SNMP counter and creates a cache file to store
last run information: timestamp and counter value.

If existing cache file is encontered on next run, change rate is calculated
and alarm is set according to WARNING and CRITICAL levels.

##Applications

Typically, this plug-in is used to monitor counters like if(In|Out)Errors, if(In|Out)Discards and if(In|Out)Octets (for high-capacity interfaces, you need to use ifHC(In|Out)Octets).

##Example command definition:

```
define command {
    command_name check_counter
    command_line /usr/lib/nagios/plugins/check_snmp -H '$HOSTADDRESS$' -C '$ARG1$' -o '$ARG2$' -w '$ARG3$' -c '$ARG4$'
 }
```

##Example service definition:

```
define service {
    host_name Host1
    service_description Gi0/1 ifInDiscards
    check_command check_counter!public!1.3.6.1.2.1.2.2.1.13.1!1!2
    use generic-service
    notification_interval 0
 }
```
