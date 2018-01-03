###  heketi安装在openshiftcluster的master节点

``` 

yum install heketi heketi-client –y

ssh-keygen -f /etc/heketi/heketi_key -t rsa -N ''
ssh-copy-id -i /etc/heketi/heketi_key.pub root@172.16.100.237
ssh-copy-id -i /etc/heketi/heketi_key.pub root@172.16.100.238
ssh-copy-id -i /etc/heketi/heketi_key.pub root@172.16.100.239
chown heketi:heketi /etc/heketi/heketi_key* 


```

### heketi.json

```
{
   "_port_comment":"Heketi Server Port Number",
   "port":"8080",
   "_use_auth":"Enable JWT authorization. Please enable for deployment",
   "use_auth":false,
   "_jwt":"Private keys for access",
   "jwt":{
      "_admin":"Admin has access to all APIs",
      "admin":{
         "key":"My Secret"
      },
      "_user":"User only has access to /volumes endpoint",
      "user":{
         "key":"My Secret"
      }
   },
   "_glusterfs_comment":"GlusterFS Configuration",
   "glusterfs":{
      "_executor_comment":[
         "Execute plugin. Possible choices: mock, ssh",
         "mock: This setting is used for testing and development.",
         " It will not send commands to any node.",
         "ssh: This setting will notify Heketi to ssh to the nodes.",
         " It will need the values in sshexec to be configured.",
         "kubernetes: Communicate with GlusterFS containers over",
         " Kubernetes exec api."
      ],
      "executor":"ssh",
      "_sshexec_comment":"SSH username and private key file information",
      "sshexec":{
         "keyfile":"/etc/heketi/heketi_key",
         "user":"root",
         "port":"22",
         "fstab":"/etc/fstab"
      },
      "_kubeexec_comment":"Kubernetes configuration",
      "kubeexec":{
         "host":"https://kubernetes.host:8443",
         "cert":"/path/to/crt.file",
         "insecure":false,
         "user":"kubernetes username",
         "password":"password for kubernetes user",
         "namespace":"OpenShift project or Kubernetes namespace",
         "fstab":"Optional: Specify fstab file on node. Default is /etc/fstab"
      },
      "_db_comment":"Database file name",
      "db":"/var/lib/heketi/heketi.db",
      "_loglevel_comment":[
         "Set log level. Choices are:",
         " none, critical, error, warning, info, debug",
         "Default is warning"
      ],
      "loglevel":"debug"
   }
}

```

### 启动heket

```
systemctl enable heketi
systemctl restart heketi

```
### 测试是否在运行
```
curl http://glusterfs01.paas.com:8080/hello
```
