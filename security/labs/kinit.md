# Kerberos Authentication

Created `spinatelli` with
```
[ec2-user@ip-172-0-0-4 ~]$ sudo kadmin.local
Authenticating as principal root/admin@EU-CENTRAL-1.COMPUTE.INTERNAL with password.
kadmin.local:  addprinc spinatelli@EU-CENTRAL-1.COMPUTE.INTERNAL
WARNING: no policy specified for spinatelli@EU-CENTRAL-1.COMPUTE.INTERNAL; defaulting to no policy
Enter password for principal "spinatelli@EU-CENTRAL-1.COMPUTE.INTERNAL":
Re-enter password for principal "spinatelli@EU-CENTRAL-1.COMPUTE.INTERNAL":
Principal "spinatelli@EU-CENTRAL-1.COMPUTE.INTERNAL" created.
```

Authenticated with
```
[ec2-user@ip-172-0-0-4 ~]$ kinit spinatelli@EU-CENTRAL-1.COMPUTE.INTERNAL
Password for spinatelli@EU-CENTRAL-1.COMPUTE.INTERNAL:
```

`klist` output:

```
[ec2-user@ip-172-0-0-4 ~]$ klist
Ticket cache: FILE:/tmp/krb5cc_1000
Default principal: spinatelli@EU-CENTRAL-1.COMPUTE.INTERNAL

Valid starting       Expires              Service principal
11/16/2016 11:30:55  11/17/2016 11:30:55  krbtgt/EU-CENTRAL-1.COMPUTE.INTERNAL@EU-CENTRAL-1.COMPUTE.INTERNAL
        renew until 11/23/2016 11:30:55
```