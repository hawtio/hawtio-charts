# HawtIO Helm Charts Repository

A development repository for making available development and snapshot versions of HawtIO applications, including [HawtIO-Online](https://github.com/hawtio/hawtio-online) and [HawtIO Console Plugin for OpenShift](https://github.com/hawtio/hawtio-online-console-plugin).

## Hawtio Console Plugin for OpenShift

The plugin provides extensions to the OpenShift console embedding the HawtIO console.

#### Pre-Requisites
- Full access to the OpenShift cluster;
- Logged-in to a namespace with deploy and pod creation privileges.

#### Installation

1. Add the chart repository to the local helm [configuration](https://helm.sh/docs/helm/helm_repo_add):
```
$ helm repo add hawtio https://hawtio.github.io/hawtio-charts
```

2. Confirm the addition of the repository:
```
$ helm repo list

NAME    URL                                   
hawtio  https://hawtio.github.io/hawtio-charts
```

3. List the contents of the helm repository using the helm [search](https://helm.sh/docs/helm/helm_search_repo) command (the `--devel` switch is required due to the versions being development releases):
```
$ helm search repo hawtio --devel

NAME                                    CHART VERSION   APP VERSION     DESCRIPTION                                       
hawtio/hawtio-online-console-plugin     0.4.0-alpha2    0.4.0-alpha2    A Helm chart for installing the OpenShift Conso...
```

4. Install the `hawtio-online-console-plugin` using the helm [install](https://helm.sh/docs/helm/helm_install) command: 
```
$ helm install --devel hawtio-online-console-plugin hawtio/hawtio-online-console-plugin

NAME: hawtio-online-console-plugin
LAST DEPLOYED: Mon Jul  7 11:51:08 2025
NAMESPACE: hawtio
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
Thank you for installing hawtio-online-console-plugin.

The release is named hawtio-online-console-plugin.

To learn more about the release, try:

  $ helm status hawtio-online-console-plugin
  $ helm get all hawtio-online-console-plugin

To learn more about hawtio, please visit https://hawt.io.
```

5. The plugin pods and services should be installed into the cluster:
```
$ oc get deploy
NAME                                   READY   UP-TO-DATE   AVAILABLE   AGE
hawtio-online-console-plugin           1/1     1            1           1h
hawtio-online-console-plugin-gateway   1/1     1            1           1h

$ oc get pods
NAME                                                   READY   STATUS      RESTARTS        AGE
hawtio-online-console-plugin-5d89b586d9-nr5rg          1/1     Running     0               1h
hawtio-online-console-plugin-gateway-588f958d5-vpzjg   1/1     Running     0               1h

$ oc get secrets
NAME                                                 TYPE                             DATA   AGE
builder-dockercfg-629hp                              kubernetes.io/dockercfg          1      4d21h
default-dockercfg-bdmbx                              kubernetes.io/dockercfg          1      4d21h
deployer-dockercfg-zchgk                             kubernetes.io/dockercfg          1      4d21h
hawtio-online-console-plugin-gateway-proxying        kubernetes.io/tls                2      1h
hawtio-online-console-plugin-gateway-serving         kubernetes.io/tls                2      1h
hawtio-online-console-plugin-serving                 kubernetes.io/tls                2      1h
sh.helm.release.v1.hawtio-online-console-plugin.v1   helm.sh/release.v1               1      1h

$ oc get services
NAME                                   TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)         AGE
hawtio-online-console-plugin           ClusterIP   10.217.4.161   <none>        9443/TCP        1h
hawtio-online-console-plugin-gateway   ClusterIP   10.217.5.19    <none>        8443/TCP        1h
```

---

Please see the [hawtIO console plugin repository](https://github.com/hawtio/hawtio-online-console-plugin) for further information.


