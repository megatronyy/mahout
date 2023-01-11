# PGSQL


![pigsty-ha](https://user-images.githubusercontent.com/8587410/206971583-74293d7b-d29a-4ca2-8728-75d50421c371.gif)


## Parameters

There are 9 sections, 106 parameters about [`PGSQL`](PARAM#PGSQL) module.


- [`PG_ID`](PARAM#pg_id)               : Calculate & Check Postgres Identity
- [`PG_BUSINESS`](PARAM#pg_business)   : Postgres Business Object Definition
- [`PG_INSTALL`](PARAM#pg_install)     : Install PGSQL Packages & Extensions
- [`PG_BOOTSTRAP`](PARAM#pg_bootstrap) : Init a HA Postgres Cluster with Patroni
- [`PG_PROVISION`](PARAM#pg_provision) : Create users, databases, in-database objects
- [`PG_BACKUP`](PARAM#pg_backup)       : Setup backup repo with pgbackrest
- [`PG_VIP`](PARAM#pg_vip)             : Bind an optional VIP on primary
- [`PG_DNS`](PARAM#pg_dns)             : Register DNS Record to Infra
- [`PG_EXPORTER`](PARAM#pg_exporter)   : Add Monitor for PG & PGBOUNCER



| Parameter                                                    | Section                                    |    Type     | Level | Comment                                                      |
| ------------------------------------------------------------ | ------------------------------------------ | :---------: | :---: | ------------------------------------------------------------ |
| [`pg_cluster`](PARAM#pg_cluster)                             | [`PG_ID`](PARAM#pg_id)                     |   string    |   C   | pgsql cluster name, REQUIRED identity parameter              |
| [`pg_seq`](PARAM#pg_seq)                                     | [`PG_ID`](PARAM#pg_id)                     |     int     |   I   | pgsql instance seq number, REQUIRED identity parameter       |
| [`pg_role`](PARAM#pg_role)                                   | [`PG_ID`](PARAM#pg_id)                     |    enum     |   I   | pgsql role, REQUIRED, could be primary,replica,offline       |
| [`pg_instances`](PARAM#pg_instances)                         | [`PG_ID`](PARAM#pg_id)                     |    dict     |   I   | define multiple pg instances on node in `{port:ins_vars}` format |
| [`pg_upstream`](PARAM#pg_upstream)                           | [`PG_ID`](PARAM#pg_id)                     |     ip      |   I   | repl upstream ip addr for standby cluster or cascade replica |
| [`pg_shard`](PARAM#pg_shard)                                 | [`PG_ID`](PARAM#pg_id)                     |   string    |   C   | pgsql shard name, optional identity for sharding clusters    |
| [`pg_sindex`](PARAM#pg_sindex)                               | [`PG_ID`](PARAM#pg_id)                     |     int     |   C   | pgsql shard index, optional identity for sharding clusters   |
| [`gp_role`](PARAM#gp_role)                                   | [`PG_ID`](PARAM#pg_id)                     |    enum     |   C   | greenplum role of this cluster, could be master or segment   |
| [`pg_exporters`](PARAM#pg_exporters)                         | [`PG_ID`](PARAM#pg_id)                     |    dict     |   C   | additional pg_exporters to monitor remote postgres instances |
| [`pg_offline_query`](PARAM#pg_offline_query)                 | [`PG_ID`](PARAM#pg_id)                     |    bool     |   G   | set to true to enable offline query on this instance         |
| [`pg_weight`](PARAM#pg_weight)                               | [`PG_ID`](PARAM#pg_id)                     |     int     |   G   | relative load balance weight in service, 100 by default, 0-255 |
| [`pg_users`](PARAM#pg_users)                                 | [`PG_BUSINESS`](PARAM#pg_business)         |   user[]    |   C   | postgres business users                                      |
| [`pg_databases`](PARAM#pg_databases)                         | [`PG_BUSINESS`](PARAM#pg_business)         | database[]  |   C   | postgres business databases                                  |
| [`pg_services`](PARAM#pg_services)                           | [`PG_BUSINESS`](PARAM#pg_business)         |  service[]  |   C   | postgres business services                                   |
| [`pg_hba_rules`](PARAM#pg_hba_rules)                         | [`PG_BUSINESS`](PARAM#pg_business)         |    hba[]    |   C   | business hba rules for postgres                              |
| [`pgb_hba_rules`](PARAM#pgb_hba_rules)                       | [`PG_BUSINESS`](PARAM#pg_business)         |    hba[]    |   C   | business hba rules for pgbouncer                             |
| [`pg_replication_username`](PARAM#pg_replication_username)   | [`PG_BUSINESS`](PARAM#pg_business)         |  username   |   G   | postgres replication username, `replicator` by default       |
| [`pg_replication_password`](PARAM#pg_replication_password)   | [`PG_BUSINESS`](PARAM#pg_business)         |  password   |   G   | postgres replication password, `DBUser.Replicator` by default |
| [`pg_admin_username`](PARAM#pg_admin_username)               | [`PG_BUSINESS`](PARAM#pg_business)         |  username   |   G   | postgres admin username, `dbuser_dba` by default             |
| [`pg_admin_password`](PARAM#pg_admin_password)               | [`PG_BUSINESS`](PARAM#pg_business)         |  password   |   G   | postgres admin password in plain text, `DBUser.DBA` by default |
| [`pg_monitor_username`](PARAM#pg_monitor_username)           | [`PG_BUSINESS`](PARAM#pg_business)         |  username   |   G   | postgres monitor username, `dbuser_monitor` by default       |
| [`pg_monitor_password`](PARAM#pg_monitor_password)           | [`PG_BUSINESS`](PARAM#pg_business)         |  password   |   G   | postgres monitor password, `DBUser.Monitor` by default       |
| [`pg_dbsu`](PARAM#pg_dbsu)                                   | [`PG_INSTALL`](PARAM#pg_install)           |  username   |   C   | os dbsu name, postgres by default, better not change it      |
| [`pg_dbsu_uid`](PARAM#pg_dbsu_uid)                           | [`PG_INSTALL`](PARAM#pg_install)           |     int     |   C   | os dbsu uid and gid, 26 for default postgres users and groups |
| [`pg_dbsu_sudo`](PARAM#pg_dbsu_sudo)                         | [`PG_INSTALL`](PARAM#pg_install)           |    enum     |   C   | dbsu sudo privilege, none,limit,all,nopass. limit by default |
| [`pg_dbsu_home`](PARAM#pg_dbsu_home)                         | [`PG_INSTALL`](PARAM#pg_install)           |    path     |   C   | postgresql home directory, `/var/lib/pgsql` by default       |
| [`pg_dbsu_ssh_exchange`](PARAM#pg_dbsu_ssh_exchange)         | [`PG_INSTALL`](PARAM#pg_install)           |    bool     |   C   | exchange postgres dbsu ssh key among same pgsql cluster      |
| [`pg_version`](PARAM#pg_version)                             | [`PG_INSTALL`](PARAM#pg_install)           |    enum     |   C   | postgres major version to be installed, 15 by default        |
| [`pg_bin_dir`](PARAM#pg_bin_dir)                             | [`PG_INSTALL`](PARAM#pg_install)           |    path     |   C   | postgres binary dir, `/usr/pgsql/bin` by default             |
| [`pg_log_dir`](PARAM#pg_log_dir)                             | [`PG_INSTALL`](PARAM#pg_install)           |    path     |   C   | postgres log dir, `/pg/log/postgres` by default              |
| [`pg_packages`](PARAM#pg_packages)                           | [`PG_INSTALL`](PARAM#pg_install)           |  string[]   |   C   | pg packages to be installed, `${pg_version}` will be replaced |
| [`pg_extensions`](PARAM#pg_extensions)                       | [`PG_INSTALL`](PARAM#pg_install)           |  string[]   |   C   | pg extensions to be installed, `${pg_version}` will be replaced |
| [`pg_safeguard`](PARAM#pg_safeguard)                         | [`PG_BOOTSTRAP`](PARAM#pg_bootstrap)       |    bool     | G/C/A | prevent purging running postgres instance? false by default  |
| [`pg_clean`](PARAM#pg_clean)                                 | [`PG_BOOTSTRAP`](PARAM#pg_bootstrap)       |    bool     | G/C/A | purging existing postgres during pgsql init? true by default |
| [`pg_data`](PARAM#pg_data)                                   | [`PG_BOOTSTRAP`](PARAM#pg_bootstrap)       |    path     |   C   | postgres data directory, `/pg/data` by default               |
| [`pg_fs_main`](PARAM#pg_fs_main)                             | [`PG_BOOTSTRAP`](PARAM#pg_bootstrap)       |    path     |   C   | mountpoint/path for postgres main data, `/data` by default   |
| [`pg_fs_bkup`](PARAM#pg_fs_bkup)                             | [`PG_BOOTSTRAP`](PARAM#pg_bootstrap)       |    path     |   C   | mountpoint/path for pg backup data, `/data/backup` by default |
| [`pg_storage_type`](PARAM#pg_storage_type)                   | [`PG_BOOTSTRAP`](PARAM#pg_bootstrap)       |    enum     |   C   | storage type for pg main data, SSD,HDD, SSD by default       |
| [`pg_dummy_filesize`](PARAM#pg_dummy_filesize)               | [`PG_BOOTSTRAP`](PARAM#pg_bootstrap)       |    size     |   C   | size of `/pg/dummy`, hold 64MB disk space for emergency use  |
| [`pg_listen`](PARAM#pg_listen)                               | [`PG_BOOTSTRAP`](PARAM#pg_bootstrap)       |     ip      |   C   | postgres listen address, `0.0.0.0` (all ipv4 addr) by default |
| [`pg_port`](PARAM#pg_port)                                   | [`PG_BOOTSTRAP`](PARAM#pg_bootstrap)       |    port     |   C   | postgres listen port, 5432 by default                        |
| [`pg_localhost`](PARAM#pg_localhost)                         | [`PG_BOOTSTRAP`](PARAM#pg_bootstrap)       |    path     |   C   | postgres unix socket dir for localhost connection            |
| [`pg_namespace`](PARAM#pg_namespace)                         | [`PG_BOOTSTRAP`](PARAM#pg_bootstrap)       |    path     |   C   | top level key namespace in etcd, used by patroni & vip       |
| [`patroni_enabled`](PARAM#patroni_enabled)                   | [`PG_BOOTSTRAP`](PARAM#pg_bootstrap)       |    bool     |   C   | if disabled, no postgres cluster will be created during init |
| [`patroni_mode`](PARAM#patroni_mode)                         | [`PG_BOOTSTRAP`](PARAM#pg_bootstrap)       |    enum     |   C   | patroni working mode: default,pause,remove                   |
| [`patroni_port`](PARAM#patroni_port)                         | [`PG_BOOTSTRAP`](PARAM#pg_bootstrap)       |    port     |   C   | patroni listen port, 8008 by default                         |
| [`patroni_log_dir`](PARAM#patroni_log_dir)                   | [`PG_BOOTSTRAP`](PARAM#pg_bootstrap)       |    path     |   C   | patroni log dir, `/pg/log/patroni` by default                |
| [`patroni_ssl_enabled`](PARAM#patroni_ssl_enabled)           | [`PG_BOOTSTRAP`](PARAM#pg_bootstrap)       |    bool     |   G   | secure patroni RestAPI communications with SSL?              |
| [`patroni_watchdog_mode`](PARAM#patroni_watchdog_mode)       | [`PG_BOOTSTRAP`](PARAM#pg_bootstrap)       |    enum     |   C   | patroni watchdog mode: automatic,required,off. off by default |
| [`patroni_username`](PARAM#patroni_username)                 | [`PG_BOOTSTRAP`](PARAM#pg_bootstrap)       |  username   |   C   | patroni restapi username, `postgres` by default              |
| [`patroni_password`](PARAM#patroni_password)                 | [`PG_BOOTSTRAP`](PARAM#pg_bootstrap)       |  password   |   C   | patroni restapi password, `Patroni.API` by default           |
| [`pg_conf`](PARAM#pg_conf)                                   | [`PG_BOOTSTRAP`](PARAM#pg_bootstrap)       |    enum     |   C   | config template: oltp,olap,crit,tiny. `oltp.yml` by default  |
| [`pg_max_conn`](PARAM#pg_max_conn)                           | [`PG_BOOTSTRAP`](PARAM#pg_bootstrap)       |     int     |   C   | postgres max connections, `auto` will use recommended value  |
| [`pg_shmem_ratio`](PARAM#pg_shmem_ratio)                     | [`PG_BOOTSTRAP`](PARAM#pg_bootstrap)       |    float    |   C   | postgres shared memory ratio, 0.25 by default, 0.1~0.4       |
| [`pg_rto`](PARAM#pg_rto)                                     | [`PG_BOOTSTRAP`](PARAM#pg_bootstrap)       |     int     |   C   | recovery time objective in seconds, `30s` by default         |
| [`pg_rpo`](PARAM#pg_rpo)                                     | [`PG_BOOTSTRAP`](PARAM#pg_bootstrap)       |     int     |   C   | recovery point objective in bytes, `1MiB` at most by default |
| [`pg_libs`](PARAM#pg_libs)                                   | [`PG_BOOTSTRAP`](PARAM#pg_bootstrap)       |   string    |   C   | preloaded libraries, `pg_stat_statements,auto_explain` by default |
| [`pg_delay`](PARAM#pg_delay)                                 | [`PG_BOOTSTRAP`](PARAM#pg_bootstrap)       |  interval   |   I   | replication apply delay for standby cluster leader           |
| [`pg_checksum`](PARAM#pg_checksum)                           | [`PG_BOOTSTRAP`](PARAM#pg_bootstrap)       |    bool     |   C   | enable data checksum for postgres cluster?                   |
| [`pg_pwd_enc`](PARAM#pg_pwd_enc)                             | [`PG_BOOTSTRAP`](PARAM#pg_bootstrap)       |    enum     |   C   | passwords encryption algorithm: md5,scram-sha-256            |
| [`pg_encoding`](PARAM#pg_encoding)                           | [`PG_BOOTSTRAP`](PARAM#pg_bootstrap)       |    enum     |   C   | database cluster encoding, `UTF8` by default                 |
| [`pg_locale`](PARAM#pg_locale)                               | [`PG_BOOTSTRAP`](PARAM#pg_bootstrap)       |    enum     |   C   | database cluster local, `C` by default                       |
| [`pg_lc_collate`](PARAM#pg_lc_collate)                       | [`PG_BOOTSTRAP`](PARAM#pg_bootstrap)       |    enum     |   C   | database cluster collate, `C` by default                     |
| [`pg_lc_ctype`](PARAM#pg_lc_ctype)                           | [`PG_BOOTSTRAP`](PARAM#pg_bootstrap)       |    enum     |   C   | database character type, `en_US.UTF8` by default             |
| [`pgbouncer_enabled`](PARAM#pgbouncer_enabled)               | [`PG_BOOTSTRAP`](PARAM#pg_bootstrap)       |    bool     |   C   | if disabled, pgbouncer will not be launched on pgsql host    |
| [`pgbouncer_port`](PARAM#pgbouncer_port)                     | [`PG_BOOTSTRAP`](PARAM#pg_bootstrap)       |    port     |   C   | pgbouncer listen port, 6432 by default                       |
| [`pgbouncer_log_dir`](PARAM#pgbouncer_log_dir)               | [`PG_BOOTSTRAP`](PARAM#pg_bootstrap)       |    path     |   C   | pgbouncer log dir, `/pg/log/pgbouncer` by default            |
| [`pgbouncer_auth_query`](PARAM#pgbouncer_auth_query)         | [`PG_BOOTSTRAP`](PARAM#pg_bootstrap)       |    bool     |   C   | query postgres to retrieve unlisted business users?          |
| [`pgbouncer_poolmode`](PARAM#pgbouncer_poolmode)             | [`PG_BOOTSTRAP`](PARAM#pg_bootstrap)       |    enum     |   C   | pooling mode: transaction,session,statement, transaction by default |
| [`pgbouncer_sslmode`](PARAM#pgbouncer_sslmode)               | [`PG_BOOTSTRAP`](PARAM#pg_bootstrap)       |    enum     |   C   | pgbouncer client ssl mode, disable by default                |
| [`pg_provision`](PARAM#pg_provision)                         | [`PG_PROVISION`](PARAM#pg_provision)       |    bool     |   C   | provision postgres cluster after bootstrap                   |
| [`pg_init`](PARAM#pg_init)                                   | [`PG_PROVISION`](PARAM#pg_provision)       |   string    |  G/C  | provision init script for cluster template, `pg-init` by default |
| [`pg_default_roles`](PARAM#pg_default_roles)                 | [`PG_PROVISION`](PARAM#pg_provision)       |   role[]    |  G/C  | default roles and users in postgres cluster                  |
| [`pg_default_privileges`](PARAM#pg_default_privileges)       | [`PG_PROVISION`](PARAM#pg_provision)       |  string[]   |  G/C  | default privileges when created by admin user                |
| [`pg_default_schemas`](PARAM#pg_default_schemas)             | [`PG_PROVISION`](PARAM#pg_provision)       |  string[]   |  G/C  | default schemas to be created                                |
| [`pg_default_extensions`](PARAM#pg_default_extensions)       | [`PG_PROVISION`](PARAM#pg_provision)       | extension[] |  G/C  | default extensions to be created                             |
| [`pg_reload`](PARAM#pg_reload)                               | [`PG_PROVISION`](PARAM#pg_provision)       |    bool     |   A   | reload postgres after hba changes                            |
| [`pg_default_hba_rules`](PARAM#pg_default_hba_rules)         | [`PG_PROVISION`](PARAM#pg_provision)       |    hba[]    |  G/C  | postgres default host-based authentication rules             |
| [`pgb_default_hba_rules`](PARAM#pgb_default_hba_rules)       | [`PG_PROVISION`](PARAM#pg_provision)       |    hba[]    |  G/C  | pgbouncer default host-based authentication rules            |
| [`pg_default_service_dest`](PARAM#pg_default_service_dest)   | [`PG_PROVISION`](PARAM#pg_provision)       |    enum     |  G/C  | default service destination if svc.dest='default'            |
| [`pg_default_services`](PARAM#pg_default_services)           | [`PG_PROVISION`](PARAM#pg_provision)       |  service[]  |  G/C  | postgres default service definitions                         |
| [`pgbackrest_enabled`](PARAM#pgbackrest_enabled)             | [`PG_BACKUP`](PARAM#pg_backup)             |    bool     |   C   | enable pgbackrest on pgsql host?                             |
| [`pgbackrest_clean`](PARAM#pgbackrest_clean)                 | [`PG_BACKUP`](PARAM#pg_backup)             |    bool     |   C   | remove pg backup data during init?                           |
| [`pgbackrest_log_dir`](PARAM#pgbackrest_log_dir)             | [`PG_BACKUP`](PARAM#pg_backup)             |    path     |   C   | pgbackrest log dir, `/pg/log/pgbackrest` by default          |
| [`pgbackrest_method`](PARAM#pgbackrest_method)               | [`PG_BACKUP`](PARAM#pg_backup)             |    enum     |   C   | pgbackrest repo method: local,minio,etc...                   |
| [`pgbackrest_repo`](PARAM#pgbackrest_repo)                   | [`PG_BACKUP`](PARAM#pg_backup)             |    dict     |  G/C  | pgbackrest repo: https://pgbackrest.org/configuration.html#section-repository |
| [`pg_vip_enabled`](PARAM#pg_vip_enabled)                     | [`PG_VIP`](PARAM#pg_vip)                   |    bool     |   C   | enable a l2 vip for pgsql primary? false by default          |
| [`pg_vip_address`](PARAM#pg_vip_address)                     | [`PG_VIP`](PARAM#pg_vip)                   |    cidr4    |   C   | vip address in `<ipv4>/<mask>` format, require if vip is enabled |
| [`pg_vip_interface`](PARAM#pg_vip_interface)                 | [`PG_VIP`](PARAM#pg_vip)                   |   string    |  C/I  | vip network interface to listen, eth0 by default             |
| [`pg_dns_suffix`](PARAM#pg_dns_suffix)                       | [`PG_DNS`](PARAM#pg_dns)                   |   string    |   C   | pgsql dns suffix, '' by default                              |
| [`pg_dns_target`](PARAM#pg_dns_target)                       | [`PG_DNS`](PARAM#pg_dns)                   |    enum     |   C   | auto, primary, vip, none, or ad hoc ip                       |
| [`pg_exporter_enabled`](PARAM#pg_exporter_enabled)           | [`PG_EXPORTER`](PARAM#pg_exporter)         |    bool     |   C   | enable pg_exporter on pgsql hosts?                           |
| [`pg_exporter_config`](PARAM#pg_exporter_config)             | [`PG_EXPORTER`](PARAM#pg_exporter)         |   string    |   C   | pg_exporter configuration file name                          |
| [`pg_exporter_cache_ttls`](PARAM#pg_exporter_cache_ttls)     | [`PG_EXPORTER`](PARAM#pg_exporter)         |   string    |   C   | pg_exporter collector ttl stage in seconds, '1,10,60,300' by default |
| [`pg_exporter_port`](PARAM#pg_exporter_port)                 | [`PG_EXPORTER`](PARAM#pg_exporter)         |    port     |   C   | pg_exporter listen port, 9630 by default                     |
| [`pg_exporter_params`](PARAM#pg_exporter_params)             | [`PG_EXPORTER`](PARAM#pg_exporter)         |   string    |   C   | extra url parameters for pg_exporter dsn                     |
| [`pg_exporter_url`](PARAM#pg_exporter_url)                   | [`PG_EXPORTER`](PARAM#pg_exporter)         |    pgurl    |   C   | overwrite auto-generate pg dsn if specified                  |
| [`pg_exporter_auto_discovery`](PARAM#pg_exporter_auto_discovery) | [`PG_EXPORTER`](PARAM#pg_exporter)         |    bool     |   C   | enable auto database discovery? enabled by default           |
| [`pg_exporter_exclude_database`](PARAM#pg_exporter_exclude_database) | [`PG_EXPORTER`](PARAM#pg_exporter)         |   string    |   C   | csv of database that WILL NOT be monitored during auto-discovery |
| [`pg_exporter_include_database`](PARAM#pg_exporter_include_database) | [`PG_EXPORTER`](PARAM#pg_exporter)         |   string    |   C   | csv of database that WILL BE monitored during auto-discovery |
| [`pg_exporter_connect_timeout`](PARAM#pg_exporter_connect_timeout) | [`PG_EXPORTER`](PARAM#pg_exporter)         |     int     |   C   | pg_exporter connect timeout in ms, 200 by default            |
| [`pg_exporter_options`](PARAM#pg_exporter_options)           | [`PG_EXPORTER`](PARAM#pg_exporter)         |     arg     |   C   | overwrite extra options for pg_exporter                      |
| [`pgbouncer_exporter_enabled`](PARAM#pgbouncer_exporter_enabled) | [`PG_EXPORTER`](PARAM#pg_exporter)         |    bool     |   C   | enable pgbouncer_exporter on pgsql hosts?                    |
| [`pgbouncer_exporter_port`](PARAM#pgbouncer_exporter_port)   | [`PG_EXPORTER`](PARAM#pg_exporter)         |    port     |   C   | pgbouncer_exporter listen port, 9631 by default              |
| [`pgbouncer_exporter_url`](PARAM#pgbouncer_exporter_url)     | [`PG_EXPORTER`](PARAM#pg_exporter)         |    pgurl    |   C   | overwrite auto-generate pgbouncer dsn if specified           |
| [`pgbouncer_exporter_options`](PARAM#pgbouncer_exporter_options) | [`PG_EXPORTER`](PARAM#pg_exporter)         |     arg     |   C   | overwrite extra options for pgbouncer_exporter               |