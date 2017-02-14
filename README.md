# Mysql role

Installs and configures mysql server.

Note: If you plan on using tls, certificats must be added to the server.
I recommend using ssl role for this.

## Required variables.

* mysql_ssl - weather to configure mysql with ssl connection.


## Optional variables

* mysql_ssl: Boolean - whether you wish to enable encrypotion.
* cert_directory - certificate directory where certificates should be placed. - refer to ssl role readme.
> You can then template key paths as ```{{ cert_directory }}/mysql.key```

* mysql_ssl_ca - path of the ca certificate.
* mysql_ssl_key - path of the ssl key to use
* mysql_ssl_cert - path of the ssl cert to use
* mysql_bind_address - Network address to bind to. Default 127.0.0.1
* mysql_server_id - Mysql server name - must be unique in the replication group.
* mysql_log_basename - log prefix.
* mysql_replication - Turn on mysql repplication
* mysql_repliction_user - Name of mysql replication role.
* mysql_replication_role - Mysql replication role Master/Slave
* mysql_replication_master - Mysql server name(as written in the inventory)
* mysql_replication_master_host - host address of the replication master.

## Promoting slave to master
To promote slave to master just change it's `mysql_replication_role` to "Master".
Ansible will check to see if the host is configured as slave and promote it to master.
Also do not forget to set `mysql_replication_master` and `mysql_replication_master_host` to the new host, so other slaves will start to replicate from it.
