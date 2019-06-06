# Dynamic Configuration
SkyWalking Configurations mostly are set through `application.yml` and OS system environment variables.
But some of them are supporting dynamic settings from upstream management system.

Right now, SkyWalking supports following dynamic configurations.

| Config Key | Value Description | Value Format Example |
|:----:|:----:|:----:|
|receiver-trace.default.slowDBAccessThreshold| Thresholds of slow Database statement, override `receiver-trace/default/slowDBAccessThreshold` of `applciation.yml`. | default:200,mongodb:50|


This feature depends on upstream service, so it is **OFF** as default.
```yaml
configuration:
  none:
```

## Dynamic Configuration Service, DCS
[Dynamic Configuration Service](../../../../oap-server/server-configuration/grpc-configuration-sync/src/main/proto/configuration-service.proto) 
is a gRPC service, which requires the upstream system implemented.
The SkyWalking OAP fetches the configuration from the implementation(any system), after you open this implementation like this.

```yaml
configuration:
  grpc:
    # Upstream system hostname
    host: 127.0.0.1
    # Upstream system port
    port: 9555
    #period : 60 # Unit seconds, sync period. Default fetch every 60 seconds.
    #clusterName: "default" # the name of current cluster, set the name if you want to upstream system known.  
```


## 3rd party Configuration Center
We are welcome contributions to implement this module provider to support popular configuration center, 
such as Zookeeper, etcd, Consul, Nacos. Submit issue to discuss.


