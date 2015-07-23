#zabbix_wowza

Zabbix template for Wowza Media Server

## Install
This is installed on the host you are running the zabbix agent on and that's capable of connecting to Wowza Media Server you would like to monitor.

```
$ git clone https://github.com/akomic/zabbix_wowza
$ cd zabbix_wowza
$ cp wowza_stats.py /etc/zabbix/externalscripts/wowza_stats.py && chmod 755 /etc/zabbix/externalscripts/wowza_stats.py
$ cp wowza.conf /etc/zabbix/zabbix_agentd.conf.d

```
Make sure this line is present in zabbix agent configuration file

```
Include=/etc/zabbix/zabbix_agentd.conf.d/
```

## Zabbix Configuration

- Import template into zabbix in Template section of web gui
- Add the template to the host
- Add following macros to the host on Zabbix web gui
.* {$WOWZAHOST}
...hostname or ip address of the Wowza Media Server
.* {$WOWZAUSER} 
.* {$WOWZAPASS}
...Username and password defined in the Wowza admin password file

## Wowza Media Server Configuration

Make sure that this HTTP Provider is configured in the Wowza VHost.xml file

```
<HTTPProvider>
        <BaseClass>com.wowza.wms.http.HTTPConnectionCountsXML</BaseClass>
        <RequestFilters>connectioncounts*</RequestFilters>
        <AuthenticationMethod>admin-digest</AuthenticationMethod>
</HTTPProvider>
```
