# Enabling TLS Level 1 Security

Following this procedure http://www.cloudera.com/documentation/enterprise/latest/topics/cm_sg_config_tls_encr.html without enabling TLS encyption for CM.

In Administration>Settings>Security set the "Use TLS Encryption for Agents" property to true.
Then on every Agent Host, replaced `use_tls=0` with `use_tls=1` in `/etc/cloudera-scm-agent/config.ini`

Restarted the Cloudera Manager Server with the following command to activate the TLS configuration settings.

```
sudo service cloudera-scm-server restart 
```

On every Agent host, restarted the Agent:
```
sudo service cloudera-scm-agent restart
```

After this, CM is not reachable. `tail`ing the log file of the server shows following error:
```
2016-11-16 12:12:18,068 WARN MainThread:org.mortbay.log: failed SslSelectChannelConnector@0.0.0.0:7182: java.io.FileNotFoundException: /var/lib/cloudera-scm-server/.keystore (No such file or directory)
2016-11-16 12:12:18,068 WARN MainThread:org.mortbay.log: failed Server@5d0f32ef: java.io.FileNotFoundException: /var/lib/cloudera-scm-server/.keystore (No such file or directory)
2016-11-16 12:12:18,068 ERROR MainThread:com.cloudera.server.cmf.Main: Failed to start Agent listener.
2016-11-16 12:12:18,069 ERROR MainThread:com.cloudera.server.cmf.Main: Server failed.
org.apache.avro.AvroRuntimeException: java.io.FileNotFoundException: /var/lib/cloudera-scm-server/.keystore (No such file or directory)
        at com.cloudera.server.common.HttpConnectorServer.start(HttpConnectorServer.java:89)
        at com.cloudera.server.cmf.Main.startAgentServer(Main.java:572)
        at com.cloudera.server.cmf.Main.startAvro(Main.java:483)
        at com.cloudera.server.cmf.Main.run(Main.java:620)
        at com.cloudera.server.cmf.Main.main(Main.java:217)
Caused by: java.io.FileNotFoundException: /var/lib/cloudera-scm-server/.keystore (No such file or directory)
        at java.io.FileInputStream.open0(Native Method)
        at java.io.FileInputStream.open(FileInputStream.java:195)
        at java.io.FileInputStream.<init>(FileInputStream.java:138)
        at org.mortbay.resource.FileResource.getInputStream(FileResource.java:275)
        at org.mortbay.jetty.security.SslSelectChannelConnector.createSSLContext(SslSelectChannelConnector.java:639)
        at org.mortbay.jetty.security.SslSelectChannelConnector.doStart(SslSelectChannelConnector.java:613)
        at org.mortbay.component.AbstractLifeCycle.start(AbstractLifeCycle.java:50)
        at org.mortbay.jetty.Server.doStart(Server.java:235)
        at org.mortbay.component.AbstractLifeCycle.start(AbstractLifeCycle.java:50)
        at com.cloudera.server.common.HttpConnectorServer.start(HttpConnectorServer.java:87)
        ... 4 more
2016-11-16 12:12:32,405 INFO ScmActive-0:com.cloudera.server.cmf.components.ScmActive: ScmActive completed successfully.
2016-11-16 12:13:18,473 INFO Thread-11:org.springframework.context.support.ClassPathXmlApplicationContext: Closing ApplicationContext 'rootContext': startup date [Wed Nov 16 12:11:44 EST 2016]; parent: org.springframework.context.support.GenericApplicationContext@1f2586d6
2016-11-16 12:13:18,475 INFO Thread-11:org.springframework.beans.factory.support.DefaultListableBeanFactory: Destroying singletons in org.springframework.beans.factory.support.DefaultListableBeanFactory@335f5c69: defining beans [contextApplicationContextProvider,org.springframework.beans.factory.config.PropertyPlaceholderConfigurer#0,sessionRegistry,passwordEncoder,sslHelper,securityUtils,processStalenessDetector,processStalenessInterceptor,scmParamTrackerStoreImpl,processHelper,releaseDetector,paramResolver,configHelper,dynamicServiceHandlerFactory,configWriterFactory,runnerDescriptorProcessFactory,compatibilityFactory,providesFactory,kerberosPrincProvider,auxConfigGeneratorFactory,configGeneratorFactory,peerConfigGeneratorFactory,zkServerInitListener,solrLoadBalancerConfigUpdateListener,solrAuthenticationConfigUpdateListener,hbaseThriftServerSecurityListener,hbaseRestServerSecurityListener,HBaseZkConfigUpdateListener,HBaseIndexerAuthenticationConfigUpdateListener,dssdToggleListener.PreCommit,dssdToggleListener.PostCommit,oozieLoadBalancerConfigUpdateListener,cmfSchedulerImpl,scheduleManagerImpl,diagnosticsDataUploadHelper,commandStorage,stalenessChecker,commandManager,callableFactory,dirtyParametersListener,metricSchemaGeneration,viewFactory,predefinedPlots,predefinedViews,metricSchemaManagerBean,monitoringTypesInitializer,workAggregatesConfigListener,heartbeatCheckerImpl,logSearchEventsCollectorImpl,serverLogFetcherImpl,ServerLogSearchResponse,agentLogFetcherImpl,descriptorFactory,embeddedDbManager,scmDbValueStore,firehoseRequestService,trialEventAuditor,cmServerState,clouderaManagerMetricsForwarder,currentUserManagerImpl,operationalReportsDisabledListener,licensedFeatureManager,cmUpgradeHelper,operationsManagerImpl,userSettingTransactionManagerImpl,trialEventStalenessCheckTrigger,licenseManagerImpl,navigatorDisabledListener,scmActive,serviceDataProviderBean,authorizer,actionablesProviderImpl,clientProtocolImpl,hostTemplateManagerImpl,sessionServiceImpl,idleSessionManagerImpl,beanConfiguration,cloudStatusDeterminer,jythonObjectFactoryImpl,pythonInterpreterFactory,parcelDependencyManagerImpl,localParcelManagerImpl,parcelInstallerImpl,parcelUpdateService,parcelManagerImpl,agentParcelProviderImpl,parcelStatusProviderImpl,parcelDownloaderImpl,periodicParcelTasks,parcelRepoConfigUpdateListener,parameterFactory,csdTranslationManager,mdlRegistry,csdRegistryImpl,csdManager,csdLocalRepository,validatorConfiguration,prototypeFactory,org.springframework.context.annotation.internalConfigurationAnnotationProcessor,org.springframework.context.annotation.internalAutowiredAnnotationProcessor,org.springframework.context.annotation.internalRequiredAnnotationProcessor,org.springframework.context.annotation.internalCommonAnnotationProcessor,rulesEngine,getObjectMapper,agentAsyncClient,newHeartbeatRequester,commandRequestsBean,getSupportedLocale,newServiceHandlerRegistry,newEventStoreClientFactory,newAutoUpgradeHandlerRegistry,newUpgradeHandlerRegistry,newAgentResultFetcher,newCmfEntityManager,newDatabaseSizeGauge,newCdhExecutorFactory,databaseExecutor,builtInServiceTypes,builtInRoleTypes,builtInNamesForCrossEntityAggregateMetrics,builtInMetricEntityAttributes,builtInMetricEntityTypes,uniqueFieldValidator,requiresSubdirValidator,validServiceDependencyValidator,uniqueServiceTypeValidator,uniqueRoleTypeValidator,existingServiceTypeValidator,existingRoleTypeValidator,expressionValidator,autoConfigSharesValidValidator,messageInterpolator,sdlParser,mdlParser,parcelParser,alternativesParser,permissionsParser,manifestParser,stringInterpolator,serviceDescriptorValidator,serviceMonitoringDefinitionsDescriptorValidator,descriptorVisitor,referenceValidator,parcelDescriptorValidator,alternativesDescriptorValidator,permissionsDescriptorValidator,manifestDescriptorValidator,defaultValidatorConfiguration,springConstraintValidatorFactory,validatorFactoryBean,metricNameFormatValidator,nameForCrossEntityAggregateFormatValidator,objectMapper]; parent: org.springframework.beans.factory.support.DefaultListableBeanFactory@7c9d8e2
2016-11-16 12:13:18,477 INFO Thread-11:com.cloudera.server.cmf.components.ScmActive: ScmActive shutting down.
2016-11-16 12:13:18,477 INFO metric-schema-updater:com.cloudera.cmon.components.MetricSchemaManager: Breaking from sleep in schema update thread.

```

Proceeded to restore previous state (no TLS enabled) by stopping `cloudera-scm-server` and `cloudera-scm-agent` on all nodes. Then on every Agent Host, replaced `use_tls=1` back with `use_tls=0` in `/etc/cloudera-scm-agent/config.ini`.
Since CM is not reachable anymore even if it is started, the `Use TLS Encryption for Agents` property has to be reverted in the MySQL database.

```
[ec2-user@ip-172-0-0-4 ~]$ mysql -u root -p
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 10342
Server version: 5.6.34-log MySQL Community Server (GPL)

Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> use scm
Database changed
mysql> UPDATE CONFIGS SET value='false' where attr="agent_tls";
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0
```

This restores everything back to normal.
In theory, these steps for configuring TLS for CM http://www.cloudera.com/documentation/enterprise/latest/topics/cm_sg_tls_browser.html#xd_583c10bfdbd326ba-7dae4aa6-147c30d0933--7a61 are a prerequisite of enabling TLS on the Agents, but they require generating certificates (here guide for self-signed certificates https://www.cloudera.com/documentation/enterprise/5-6-x/topics/sg_self_signed_tls.html)