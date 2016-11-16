```
{
  "timestamp" : "2016-11-16T10:00:34.178Z",
  "clusters" : [ {
    "name" : "Spinatelli",
    "version" : "CDH5",
    "services" : [ {
      "name" : "zookeeper",
      "type" : "ZOOKEEPER",
      "config" : {
        "roleTypeConfigs" : [ ],
        "items" : [ ]
      },
      "roles" : [ {
        "name" : "zookeeper-SERVER-03a4eac602be60ee5809a5f43479b13c",
        "type" : "SERVER",
        "hostRef" : {
          "hostId" : "i-60bb21dd"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "2f6045tcdm5gf0nd0uz8v3ov"
          }, {
            "name" : "serverId",
            "value" : "1"
          } ]
        }
      }, {
        "name" : "zookeeper-SERVER-10bf45b7132a71ed9c5de14ca7714536",
        "type" : "SERVER",
        "hostRef" : {
          "hostId" : "i-63bb21de"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "3l7evzzyhp8z0zeedv5lic1iz"
          }, {
            "name" : "serverId",
            "value" : "2"
          } ]
        }
      }, {
        "name" : "zookeeper-SERVER-d1e4e2dab22339faba1a74091999b06b",
        "type" : "SERVER",
        "hostRef" : {
          "hostId" : "i-62bb21df"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "ady3dm38zb8zbfkzca0q3tyv8"
          }, {
            "name" : "serverId",
            "value" : "3"
          } ]
        }
      } ],
      "displayName" : "ZooKeeper"
    }, {
      "name" : "oozie",
      "type" : "OOZIE",
      "config" : {
        "roleTypeConfigs" : [ {
          "roleType" : "OOZIE_SERVER",
          "items" : [ {
            "name" : "oozie_database_host",
            "value" : "ip-172-0-0-4.eu-central-1.compute.internal"
          }, {
            "name" : "oozie_database_password",
            "value" : "oozie"
          }, {
            "name" : "oozie_database_type",
            "value" : "mysql"
          }, {
            "name" : "oozie_database_user",
            "value" : "oozie"
          }, {
            "name" : "oozie_java_heapsize",
            "value" : "838860800"
          } ]
        } ],
        "items" : [ {
          "name" : "hive_service",
          "value" : "hive"
        }, {
          "name" : "mapreduce_yarn_service",
          "value" : "yarn"
        }, {
          "name" : "zookeeper_service",
          "value" : "zookeeper"
        } ]
      },
      "roles" : [ {
        "name" : "oozie-OOZIE_SERVER-75de3d1dd034914dc83fb84dfb2db8ff",
        "type" : "OOZIE_SERVER",
        "hostRef" : {
          "hostId" : "i-61bb21dc"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "1r0g80vqvnawgcvcu96k4mv1k"
          } ]
        }
      } ],
      "displayName" : "Oozie"
    }, {
      "name" : "hue",
      "type" : "HUE",
      "config" : {
        "roleTypeConfigs" : [ ],
        "items" : [ {
          "name" : "database_host",
          "value" : "ip-172-0-0-4.eu-central-1.compute.internal"
        }, {
          "name" : "database_password",
          "value" : "hue"
        }, {
          "name" : "database_type",
          "value" : "mysql"
        }, {
          "name" : "hive_service",
          "value" : "hive"
        }, {
          "name" : "hue_webhdfs",
          "value" : "hdfs-HTTPFS-03a4eac602be60ee5809a5f43479b13c"
        }, {
          "name" : "oozie_service",
          "value" : "oozie"
        }, {
          "name" : "zookeeper_service",
          "value" : "zookeeper"
        } ]
      },
      "roles" : [ {
        "name" : "hue-HUE_SERVER-75de3d1dd034914dc83fb84dfb2db8ff",
        "type" : "HUE_SERVER",
        "hostRef" : {
          "hostId" : "i-61bb21dc"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "2m4axi7ulsbmmblerdwp6wprc"
          }, {
            "name" : "secret_key",
            "value" : "fKd1iN5SCkyDxei7EnTIz2SZGRLF2f"
          } ]
        }
      } ],
      "displayName" : "Hue"
    }, {
      "name" : "hdfs",
      "type" : "HDFS",
      "config" : {
        "roleTypeConfigs" : [ {
          "roleType" : "DATANODE",
          "items" : [ {
            "name" : "datanode_java_heapsize",
            "value" : "1073741824"
          }, {
            "name" : "dfs_data_dir_list",
            "value" : "/dfs/dn"
          }, {
            "name" : "dfs_datanode_du_reserved",
            "value" : "10736157900"
          }, {
            "name" : "dfs_datanode_max_locked_memory",
            "value" : "4294967296"
          }, {
            "name" : "rm_cpu_shares",
            "value" : "200"
          }, {
            "name" : "rm_io_weight",
            "value" : "100"
          } ]
        }, {
          "roleType" : "GATEWAY",
          "items" : [ {
            "name" : "dfs_client_use_trash",
            "value" : "true"
          } ]
        }, {
          "roleType" : "JOURNALNODE",
          "items" : [ {
            "name" : "dfs_journalnode_edits_dir",
            "value" : "/dfs/jn"
          }, {
            "name" : "role_health_suppression_journal_node_fsync_latency",
            "value" : "true"
          } ]
        }, {
          "roleType" : "NAMENODE",
          "items" : [ {
            "name" : "dfs_name_dir_list",
            "value" : "/dfs/nn"
          }, {
            "name" : "dfs_namenode_servicerpc_address",
            "value" : "8022"
          } ]
        }, {
          "roleType" : "SECONDARYNAMENODE",
          "items" : [ {
            "name" : "fs_checkpoint_dir_list",
            "value" : "/dfs/snn"
          } ]
        } ],
        "items" : [ {
          "name" : "dfs_client_use_datanode_hostname",
          "value" : "true"
        }, {
          "name" : "dfs_ha_fencing_cloudera_manager_secret_key",
          "value" : "GV3YqNztNzGzir7gbhyyBaBTKewJDK"
        }, {
          "name" : "dfs_ha_fencing_methods",
          "value" : "shell(true)"
        }, {
          "name" : "fc_authorization_secret_key",
          "value" : "X6CEYU5YN78Z7KtVaNo3HlTEJdHmJC"
        }, {
          "name" : "http_auth_signature_secret",
          "value" : "zwa1G9kh9U3yz4QZGH5Y6OWA4of2pZ"
        }, {
          "name" : "rm_dirty",
          "value" : "false"
        }, {
          "name" : "rm_last_allocation_percentage",
          "value" : "10"
        }, {
          "name" : "zookeeper_service",
          "value" : "zookeeper"
        } ]
      },
      "roles" : [ {
        "name" : "hdfs-BALANCER-75de3d1dd034914dc83fb84dfb2db8ff",
        "type" : "BALANCER",
        "hostRef" : {
          "hostId" : "i-61bb21dc"
        },
        "config" : {
          "items" : [ ]
        }
      }, {
        "name" : "hdfs-DATANODE-03a4eac602be60ee5809a5f43479b13c",
        "type" : "DATANODE",
        "hostRef" : {
          "hostId" : "i-60bb21dd"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "cxj7dk8o2zgcx3veom506tvzi"
          } ]
        }
      }, {
        "name" : "hdfs-DATANODE-10bf45b7132a71ed9c5de14ca7714536",
        "type" : "DATANODE",
        "hostRef" : {
          "hostId" : "i-63bb21de"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "13xtd9wilpq5ccuejl4prh7sx"
          } ]
        }
      }, {
        "name" : "hdfs-DATANODE-d1e4e2dab22339faba1a74091999b06b",
        "type" : "DATANODE",
        "hostRef" : {
          "hostId" : "i-62bb21df"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "f1cjafx7irei0n77nrb7v5kvp"
          } ]
        }
      }, {
        "name" : "hdfs-FAILOVERCONTROLLER-61e981aaeff2cf669d214a8dfe3316c5",
        "type" : "FAILOVERCONTROLLER",
        "hostRef" : {
          "hostId" : "i-66bb21db"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "arvw5lpkoyd6hmup24x5l85f5"
          } ]
        }
      }, {
        "name" : "hdfs-FAILOVERCONTROLLER-75de3d1dd034914dc83fb84dfb2db8ff",
        "type" : "FAILOVERCONTROLLER",
        "hostRef" : {
          "hostId" : "i-61bb21dc"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "bx7n6018zfi93pfheg613u698"
          } ]
        }
      }, {
        "name" : "hdfs-HTTPFS-03a4eac602be60ee5809a5f43479b13c",
        "type" : "HTTPFS",
        "hostRef" : {
          "hostId" : "i-60bb21dd"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "d8b21z0o6xjqpn1zfhkdm4yy8"
          } ]
        }
      }, {
        "name" : "hdfs-JOURNALNODE-03a4eac602be60ee5809a5f43479b13c",
        "type" : "JOURNALNODE",
        "hostRef" : {
          "hostId" : "i-60bb21dd"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "as70r1yyoad99omfktw97kmz6"
          } ]
        }
      }, {
        "name" : "hdfs-JOURNALNODE-61e981aaeff2cf669d214a8dfe3316c5",
        "type" : "JOURNALNODE",
        "hostRef" : {
          "hostId" : "i-66bb21db"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "2bj5wgqx7xl2ezbtf2vp8oj41"
          } ]
        }
      }, {
        "name" : "hdfs-JOURNALNODE-75de3d1dd034914dc83fb84dfb2db8ff",
        "type" : "JOURNALNODE",
        "hostRef" : {
          "hostId" : "i-61bb21dc"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "6lbwjqnprnk1y6theuxsc3zr9"
          } ]
        }
      }, {
        "name" : "hdfs-NAMENODE-61e981aaeff2cf669d214a8dfe3316c5",
        "type" : "NAMENODE",
        "hostRef" : {
          "hostId" : "i-66bb21db"
        },
        "config" : {
          "items" : [ {
            "name" : "autofailover_enabled",
            "value" : "true"
          }, {
            "name" : "dfs_federation_namenode_nameservice",
            "value" : "bcservice1"
          }, {
            "name" : "dfs_namenode_quorum_journal_name",
            "value" : "bcservice1"
          }, {
            "name" : "namenode_id",
            "value" : "200"
          }, {
            "name" : "role_jceks_password",
            "value" : "8mcxo5pqpvrdqybdk88eh8fl"
          } ]
        }
      }, {
        "name" : "hdfs-NAMENODE-75de3d1dd034914dc83fb84dfb2db8ff",
        "type" : "NAMENODE",
        "hostRef" : {
          "hostId" : "i-61bb21dc"
        },
        "config" : {
          "items" : [ {
            "name" : "autofailover_enabled",
            "value" : "true"
          }, {
            "name" : "dfs_federation_namenode_nameservice",
            "value" : "bcservice1"
          }, {
            "name" : "dfs_namenode_quorum_journal_name",
            "value" : "bcservice1"
          }, {
            "name" : "namenode_id",
            "value" : "232"
          }, {
            "name" : "role_jceks_password",
            "value" : "99ga4acrov6rl9g4h2hl4bajr"
          } ]
        }
      }, {
        "name" : "hdfs-NFSGATEWAY-10bf45b7132a71ed9c5de14ca7714536",
        "type" : "NFSGATEWAY",
        "hostRef" : {
          "hostId" : "i-63bb21de"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "5itefvmntxa7zgipfcnnq290a"
          } ]
        }
      } ],
      "displayName" : "HDFS"
    }, {
      "name" : "yarn",
      "type" : "YARN",
      "config" : {
        "roleTypeConfigs" : [ {
          "roleType" : "GATEWAY",
          "items" : [ {
            "name" : "mapred_reduce_tasks",
            "value" : "6"
          }, {
            "name" : "mapred_submit_replication",
            "value" : "1"
          } ]
        }, {
          "roleType" : "JOBHISTORY",
          "items" : [ {
            "name" : "mr2_jobhistory_java_heapsize",
            "value" : "838860800"
          } ]
        }, {
          "roleType" : "NODEMANAGER",
          "items" : [ {
            "name" : "rm_cpu_shares",
            "value" : "1800"
          }, {
            "name" : "rm_io_weight",
            "value" : "900"
          }, {
            "name" : "yarn_nodemanager_heartbeat_interval_ms",
            "value" : "100"
          }, {
            "name" : "yarn_nodemanager_local_dirs",
            "value" : "/yarn/nm"
          }, {
            "name" : "yarn_nodemanager_log_dirs",
            "value" : "/yarn/container-logs"
          }, {
            "name" : "yarn_nodemanager_resource_cpu_vcores",
            "value" : "3"
          }, {
            "name" : "yarn_nodemanager_resource_memory_mb",
            "value" : "2610"
          } ]
        }, {
          "roleType" : "RESOURCEMANAGER",
          "items" : [ {
            "name" : "yarn_scheduler_maximum_allocation_mb",
            "value" : "2610"
          }, {
            "name" : "yarn_scheduler_maximum_allocation_vcores",
            "value" : "3"
          } ]
        } ],
        "items" : [ {
          "name" : "hdfs_service",
          "value" : "hdfs"
        }, {
          "name" : "rm_dirty",
          "value" : "false"
        }, {
          "name" : "rm_last_allocation_percentage",
          "value" : "90"
        }, {
          "name" : "yarn_service_cgroups",
          "value" : "false"
        }, {
          "name" : "yarn_service_lce_always",
          "value" : "false"
        }, {
          "name" : "zk_authorization_secret_key",
          "value" : "tuM7yhAusKhkBcXsLdFo2pBDGebLJK"
        }, {
          "name" : "zookeeper_service",
          "value" : "zookeeper"
        } ]
      },
      "roles" : [ {
        "name" : "yarn-GATEWAY-61e981aaeff2cf669d214a8dfe3316c5",
        "type" : "GATEWAY",
        "hostRef" : {
          "hostId" : "i-66bb21db"
        },
        "config" : {
          "items" : [ ]
        }
      }, {
        "name" : "yarn-JOBHISTORY-10bf45b7132a71ed9c5de14ca7714536",
        "type" : "JOBHISTORY",
        "hostRef" : {
          "hostId" : "i-63bb21de"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "3otgpbhdk4ubdy7r9t6g58qde"
          } ]
        }
      }, {
        "name" : "yarn-NODEMANAGER-03a4eac602be60ee5809a5f43479b13c",
        "type" : "NODEMANAGER",
        "hostRef" : {
          "hostId" : "i-60bb21dd"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "dwgimnwvi09b9tq5hc11fkspn"
          } ]
        }
      }, {
        "name" : "yarn-NODEMANAGER-75de3d1dd034914dc83fb84dfb2db8ff",
        "type" : "NODEMANAGER",
        "hostRef" : {
          "hostId" : "i-61bb21dc"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "3b05q5pmrr5b52zbpnqivi3o8"
          } ]
        }
      }, {
        "name" : "yarn-NODEMANAGER-d1e4e2dab22339faba1a74091999b06b",
        "type" : "NODEMANAGER",
        "hostRef" : {
          "hostId" : "i-62bb21df"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "e7xr7at2k83jp5gdz8ea7dmby"
          } ]
        }
      }, {
        "name" : "yarn-RESOURCEMANAGER-10bf45b7132a71ed9c5de14ca7714536",
        "type" : "RESOURCEMANAGER",
        "hostRef" : {
          "hostId" : "i-63bb21de"
        },
        "config" : {
          "items" : [ {
            "name" : "rm_id",
            "value" : "222"
          }, {
            "name" : "role_jceks_password",
            "value" : "7tx7p25mlwo4nxmxt2plnz16w"
          } ]
        }
      } ],
      "displayName" : "YARN (MR2 Included)"
    }, {
      "name" : "hive",
      "type" : "HIVE",
      "config" : {
        "roleTypeConfigs" : [ {
          "roleType" : "HIVEMETASTORE",
          "items" : [ {
            "name" : "hive_metastore_java_heapsize",
            "value" : "838860800"
          } ]
        }, {
          "roleType" : "HIVESERVER2",
          "items" : [ {
            "name" : "hiveserver2_java_heapsize",
            "value" : "1981808640"
          }, {
            "name" : "hiveserver2_spark_driver_memory",
            "value" : "966367641"
          }, {
            "name" : "hiveserver2_spark_executor_cores",
            "value" : "4"
          }, {
            "name" : "hiveserver2_spark_executor_memory",
            "value" : "2189898547"
          }, {
            "name" : "hiveserver2_spark_yarn_driver_memory_overhead",
            "value" : "102"
          }, {
            "name" : "hiveserver2_spark_yarn_executor_memory_overhead",
            "value" : "368"
          } ]
        } ],
        "items" : [ {
          "name" : "hive_metastore_database_host",
          "value" : "ip-172-0-0-4.eu-central-1.compute.internal"
        }, {
          "name" : "hive_metastore_database_password",
          "value" : "hive"
        }, {
          "name" : "mapreduce_yarn_service",
          "value" : "yarn"
        }, {
          "name" : "zookeeper_service",
          "value" : "zookeeper"
        } ]
      },
      "roles" : [ {
        "name" : "hive-GATEWAY-03a4eac602be60ee5809a5f43479b13c",
        "type" : "GATEWAY",
        "hostRef" : {
          "hostId" : "i-60bb21dd"
        },
        "config" : {
          "items" : [ ]
        }
      }, {
        "name" : "hive-GATEWAY-10bf45b7132a71ed9c5de14ca7714536",
        "type" : "GATEWAY",
        "hostRef" : {
          "hostId" : "i-63bb21de"
        },
        "config" : {
          "items" : [ ]
        }
      }, {
        "name" : "hive-GATEWAY-61e981aaeff2cf669d214a8dfe3316c5",
        "type" : "GATEWAY",
        "hostRef" : {
          "hostId" : "i-66bb21db"
        },
        "config" : {
          "items" : [ ]
        }
      }, {
        "name" : "hive-GATEWAY-75de3d1dd034914dc83fb84dfb2db8ff",
        "type" : "GATEWAY",
        "hostRef" : {
          "hostId" : "i-61bb21dc"
        },
        "config" : {
          "items" : [ ]
        }
      }, {
        "name" : "hive-GATEWAY-d1e4e2dab22339faba1a74091999b06b",
        "type" : "GATEWAY",
        "hostRef" : {
          "hostId" : "i-62bb21df"
        },
        "config" : {
          "items" : [ ]
        }
      }, {
        "name" : "hive-HIVEMETASTORE-d1e4e2dab22339faba1a74091999b06b",
        "type" : "HIVEMETASTORE",
        "hostRef" : {
          "hostId" : "i-62bb21df"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "d3ynjz4kf89g7sa21m89b850b"
          } ]
        }
      }, {
        "name" : "hive-HIVESERVER2-d1e4e2dab22339faba1a74091999b06b",
        "type" : "HIVESERVER2",
        "hostRef" : {
          "hostId" : "i-62bb21df"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "7u03fc8gvww4rd0cfbnkhk3f7"
          } ]
        }
      } ],
      "displayName" : "Hive"
    } ]
  } ],
  "hosts" : [ {
    "hostId" : "i-60bb21dd",
    "ipAddress" : "172.0.0.12",
    "hostname" : "ip-172-0-0-12.eu-central-1.compute.internal",
    "rackId" : "/default",
    "config" : {
      "items" : [ ]
    }
  }, {
    "hostId" : "i-63bb21de",
    "ipAddress" : "172.0.0.13",
    "hostname" : "ip-172-0-0-13.eu-central-1.compute.internal",
    "rackId" : "/default",
    "config" : {
      "items" : [ ]
    }
  }, {
    "hostId" : "i-62bb21df",
    "ipAddress" : "172.0.0.14",
    "hostname" : "ip-172-0-0-14.eu-central-1.compute.internal",
    "rackId" : "/default",
    "config" : {
      "items" : [ ]
    }
  }, {
    "hostId" : "i-66bb21db",
    "ipAddress" : "172.0.0.4",
    "hostname" : "ip-172-0-0-4.eu-central-1.compute.internal",
    "rackId" : "/default",
    "config" : {
      "items" : [ ]
    }
  }, {
    "hostId" : "i-61bb21dc",
    "ipAddress" : "172.0.0.5",
    "hostname" : "ip-172-0-0-5.eu-central-1.compute.internal",
    "rackId" : "/default",
    "config" : {
      "items" : [ ]
    }
  } ],
  "users" : [ {
    "name" : "__cloudera_internal_user__e327e2a7-1829-4bb6-a3b3-11540eb4ca60",
    "roles" : [ "ROLE_USER" ],
    "pwHash" : "a6629acb1561556275831cb66ec428a2e5e15c361f29f2640e04c31299229609",
    "pwSalt" : -1420128928829708629,
    "pwLogin" : true
  }, {
    "name" : "__cloudera_internal_user__mgmt-ACTIVITYMONITOR-61e981aaeff2cf669d214a8dfe3316c5",
    "roles" : [ "ROLE_USER" ],
    "pwHash" : "74ec7c3e5fd833672cc3d8a18b6ce586cb8b7352a944b5cecacb739258dc775a",
    "pwSalt" : 3921346237744379211,
    "pwLogin" : true
  }, {
    "name" : "__cloudera_internal_user__mgmt-EVENTSERVER-61e981aaeff2cf669d214a8dfe3316c5",
    "roles" : [ "ROLE_USER" ],
    "pwHash" : "be1ebe39a23157d832c41d71e23470e24baea0801564d7c3fe1622412546dda1",
    "pwSalt" : -1841120692047748951,
    "pwLogin" : true
  }, {
    "name" : "__cloudera_internal_user__mgmt-HOSTMONITOR-61e981aaeff2cf669d214a8dfe3316c5",
    "roles" : [ "ROLE_USER" ],
    "pwHash" : "59a703e27ca3e5d5872c27c5d350196c5a65570e9b2ec923f8a0690caedba0db",
    "pwSalt" : -1129581316901836313,
    "pwLogin" : true
  }, {
    "name" : "__cloudera_internal_user__mgmt-REPORTSMANAGER-61e981aaeff2cf669d214a8dfe3316c5",
    "roles" : [ "ROLE_USER" ],
    "pwHash" : "6c7cbb0c2816677241c0577fcead589feb75b98fd45c8638b4edb217a8a84af1",
    "pwSalt" : 1106258315104307970,
    "pwLogin" : true
  }, {
    "name" : "__cloudera_internal_user__mgmt-SERVICEMONITOR-61e981aaeff2cf669d214a8dfe3316c5",
    "roles" : [ "ROLE_USER" ],
    "pwHash" : "0c6294af2ce7487aa8d0fc5ca34003020d7246d8efe51f9cbf2859cb981fb3bb",
    "pwSalt" : 2838665036107037520,
    "pwLogin" : true
  }, {
    "name" : "admin",
    "roles" : [ "ROLE_LIMITED" ],
    "pwHash" : "b65ad4e40691117d350d67a61d03b0af8c70c51431f60d528af101176bb34b28",
    "pwSalt" : -7687861224236238277,
    "pwLogin" : true
  }, {
    "name" : "minotaur",
    "roles" : [ "ROLE_CONFIGURATOR" ],
    "pwHash" : "ea3af73ff2288c2e90b8754a0fdd2daaf1ed5a52ea5ec044a32b47028ded77c3",
    "pwSalt" : -3879830644715148501,
    "pwLogin" : true
  }, {
    "name" : "spinatelli",
    "roles" : [ "ROLE_ADMIN" ],
    "pwHash" : "3fe73bb9e535b698bfd65fe4e6cd4fe4ec8bc5e077b2f8ea39152cbd8de42ad2",
    "pwSalt" : -8306247532606117318,
    "pwLogin" : true
  } ],
  "versionInfo" : {
    "version" : "5.9.0",
    "buildUser" : "jenkins",
    "buildTimestamp" : "20161006-1801",
    "gitHash" : "898a5e032c080e18833dfc58180761f6ef2ea351",
    "snapshot" : false
  },
  "managementService" : {
    "name" : "mgmt",
    "type" : "MGMT",
    "config" : {
      "roleTypeConfigs" : [ {
        "roleType" : "ACTIVITYMONITOR",
        "items" : [ {
          "name" : "firehose_database_host",
          "value" : "ip-172-0-0-4.eu-central-1.compute.internal"
        }, {
          "name" : "firehose_database_name",
          "value" : "amon"
        }, {
          "name" : "firehose_database_password",
          "value" : "amon"
        }, {
          "name" : "firehose_database_user",
          "value" : "amon"
        }, {
          "name" : "firehose_heapsize",
          "value" : "838860800"
        } ]
      }, {
        "roleType" : "EVENTSERVER",
        "items" : [ {
          "name" : "event_server_heapsize",
          "value" : "838860800"
        } ]
      }, {
        "roleType" : "HOSTMONITOR",
        "items" : [ {
          "name" : "firehose_non_java_memory_bytes",
          "value" : "1610612736"
        } ]
      }, {
        "roleType" : "REPORTSMANAGER",
        "items" : [ {
          "name" : "headlamp_database_host",
          "value" : "ip-172-0-0-4.eu-central-1.compute.internal"
        }, {
          "name" : "headlamp_database_name",
          "value" : "rman"
        }, {
          "name" : "headlamp_database_password",
          "value" : "rman"
        }, {
          "name" : "headlamp_database_user",
          "value" : "rman"
        }, {
          "name" : "headlamp_heapsize",
          "value" : "838860800"
        } ]
      }, {
        "roleType" : "SERVICEMONITOR",
        "items" : [ {
          "name" : "firehose_non_java_memory_bytes",
          "value" : "1610612736"
        } ]
      } ],
      "items" : [ ]
    },
    "roles" : [ {
      "name" : "mgmt-ACTIVITYMONITOR-61e981aaeff2cf669d214a8dfe3316c5",
      "type" : "ACTIVITYMONITOR",
      "hostRef" : {
        "hostId" : "i-66bb21db"
      },
      "config" : {
        "items" : [ {
          "name" : "role_jceks_password",
          "value" : "an8fhokgiae0e3urus45tcu0d"
        } ]
      }
    }, {
      "name" : "mgmt-ALERTPUBLISHER-d1e4e2dab22339faba1a74091999b06b",
      "type" : "ALERTPUBLISHER",
      "hostRef" : {
        "hostId" : "i-62bb21df"
      },
      "config" : {
        "items" : [ {
          "name" : "role_jceks_password",
          "value" : "7id4u3cu3wta479t2dq4kse89"
        } ]
      }
    }, {
      "name" : "mgmt-EVENTSERVER-61e981aaeff2cf669d214a8dfe3316c5",
      "type" : "EVENTSERVER",
      "hostRef" : {
        "hostId" : "i-66bb21db"
      },
      "config" : {
        "items" : [ {
          "name" : "role_jceks_password",
          "value" : "eqo6nbcx6wi692d7gso15naop"
        } ]
      }
    }, {
      "name" : "mgmt-HOSTMONITOR-61e981aaeff2cf669d214a8dfe3316c5",
      "type" : "HOSTMONITOR",
      "hostRef" : {
        "hostId" : "i-66bb21db"
      },
      "config" : {
        "items" : [ {
          "name" : "role_jceks_password",
          "value" : "c1x0b8tgdywyla0bwdw8ctiy3"
        } ]
      }
    }, {
      "name" : "mgmt-REPORTSMANAGER-61e981aaeff2cf669d214a8dfe3316c5",
      "type" : "REPORTSMANAGER",
      "hostRef" : {
        "hostId" : "i-66bb21db"
      },
      "config" : {
        "items" : [ {
          "name" : "role_jceks_password",
          "value" : "c1xzmqk1tgigvn4k45mmhmlhy"
        } ]
      }
    }, {
      "name" : "mgmt-SERVICEMONITOR-61e981aaeff2cf669d214a8dfe3316c5",
      "type" : "SERVICEMONITOR",
      "hostRef" : {
        "hostId" : "i-66bb21db"
      },
      "config" : {
        "items" : [ {
          "name" : "role_jceks_password",
          "value" : "87wyxlkdxv2fiztsgcb7yb9dg"
        } ]
      }
    } ],
    "displayName" : "Cloudera Management Service"
  },
  "managerSettings" : {
    "items" : [ {
      "name" : "CLUSTER_STATS_START",
      "value" : "10/23/2012 9:10"
    }, {
      "name" : "PUBLIC_CLOUD_STATUS",
      "value" : "ON_PUBLIC_CLOUD"
    }, {
      "name" : "REMOTE_PARCEL_REPO_URLS",
      "value" : "https://archive.cloudera.com/cdh5/parcels/{latest_supported}/,https://archive.cloudera.com/cdh4/parcels/latest/,https://archive.cloudera.com/impala/parcels/latest/,https://archive.cloudera.com/search/parcels/latest/,https://archive.cloudera.com/accumulo/parcels/1.4/,https://archive.cloudera.com/accumulo-c5/parcels/latest/,https://archive.cloudera.com/navigator-keytrustee5/parcels/latest/,https://archive.cloudera.com/spark/parcels/latest/,https://archive.cloudera.com/sqoop-connectors/parcels/latest/,http://ip-172-0-0-5.eu-central-1.compute.internal/parcel_repo/kafka-2.0.2.5"
    } ]
  }
}
```