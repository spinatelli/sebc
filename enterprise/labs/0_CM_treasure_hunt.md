# Answers

1. The small-jobs "ubertask" optimization runs "sufficiently small" jobs sequentially within a single JVM. "Small" is defined by the maxmaps, maxreduces, and maxbytes settings.
2. Administration->Settings->default_realm property
3. All core CDH services have a property for enabling Kerberos: HDFS, YARN, Oozie, Zookeeper, Hue, Hive, Cloudera Management Services
4. The Cloudera Manager upgrade wizard can upgrade the agent software (and, optionally, the JDK), or you can install the agent and JDK software manually.
5. SELECT cpu_system_rate + cpu_user_rate WHERE serviceName = hue
6. Hive Gateway, Hive Metastore Server, HiveServer2
7. Following steps are needed to integrate Kerberos with CM:
    * There is a working Kerberos key distribution center (KDC) available and reachable
    * `openldap-clients` package is installed on the Cloudera Manager Server host
    * `krb5-workstation`, `krb5-libs` packages are installed on ALL hosts
    * Oozie and Hue require that the realm support renewable tickets
    * If using AES-256 Encryption, install the JCE Policy File
    * Get or create a Kerberos Principal for the Cloudera Manager Server
    * Enabling Kerberos Using the Wizard
  After enabling it:
    * Create the HDFS Superuser
    * Get or create a Kerberos Principal for each user account
    * Prepare the cluster for each user (setting up Linux users etc)