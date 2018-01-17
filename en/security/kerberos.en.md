## Kerberos ##

Kerberos is a computer network authentication protocol that works on the basis of tickets. If the platform which installed KAP enable the protocol, some configurations need to be changed to support that.

### KAP Configurations ###

In the properties file：`$KYLIN_HOME/conf/kylin.properties`, there are some parameters about kerberos which need to be noticed.

Mandatory parameters：

   - kap.kerberos.enabled: enabled kerberos protocol. The value could be true or false (default).
   - kap.kerberos.platform: certification platform. The default value is Standard.
   - kap.kerberos.principal:  the name of principal
   - kap.kerberos.keytab:  the file name of keytab

Optional parameters：

   - kap.kerberos.ticket.refresh.interval.minutes: the refresh interval of tickets. The unit is minute and the default value is 720 minutes.
   - kap.kerberos.krb5.conf: the config file name of kerbero. Default value is krb5.conf
   - kap.kerberos.cache: the name of ticket cache file.  Default value is kap_kerberos.cache.

### Standard Configuration ###

1. In the node (installed yarn) of NodeManager, the user which corresponds kerberos need to be added.

   For example:

   The kerberos user(kylin) also need to be exist in the operation system of NodeManager.

2. Parameters about kerberos configuration:

   - kap.kerberos.enabled=true
   - kap.kerberos.platform=Standard
   - kap.kerberos.principal={your principal name}
   - kap.kerberos.keytab={your keytab name}

3. Move the keytab file into`$KYLIN_HOME/conf`.  
