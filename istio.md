# Istio install and test.


### Install

login to my Kubenetes cluster master node and check the status of the cluster. 

Everything is normal and all other pods are cleaned already. 

To install the latest istio release. 

```
curl -L https://git.io/getLatestIstio | sh -
```

And here is the output. 

```
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0
100  1456  100  1456    0     0   3039      0 --:--:-- --:--:-- --:--:--  3039
Downloading istio-1.0.2 from https://github.com/istio/istio/releases/download/1.0.2/istio-1.0.2-linux.tar.gz ...
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   614    0   614    0     0   2590      0 --:--:-- --:--:-- --:--:--  2590
100 14.1M  100 14.1M    0     0  2004k      0  0:00:07  0:00:07 --:--:-- 2178k
Downloaded into istio-1.0.2:
bin  install  istio.VERSION  LICENSE  README.md  samples  tools
Add /home/steve/istio-1.0.2/bin to your path; e.g copy paste in your shell and/or ~/.profile:
export PATH="$PATH:/home/steve/istio-1.0.2/bin"

```

Based on the output above, add the export to the ~/.profile

Go to the istio-1.0.2 folder and run the following command

```
kubectl apply -f install/kubernetes/helm/istio/templates/crds.yaml
```

Here is the output. 

```
customresourcedefinition.apiextensions.k8s.io/virtualservices.networking.istio.io created
customresourcedefinition.apiextensions.k8s.io/destinationrules.networking.istio.io created
customresourcedefinition.apiextensions.k8s.io/serviceentries.networking.istio.io created
customresourcedefinition.apiextensions.k8s.io/gateways.networking.istio.io created
customresourcedefinition.apiextensions.k8s.io/envoyfilters.networking.istio.io created
customresourcedefinition.apiextensions.k8s.io/policies.authentication.istio.io created
customresourcedefinition.apiextensions.k8s.io/meshpolicies.authentication.istio.io created
customresourcedefinition.apiextensions.k8s.io/httpapispecbindings.config.istio.io created
customresourcedefinition.apiextensions.k8s.io/httpapispecs.config.istio.io created
customresourcedefinition.apiextensions.k8s.io/quotaspecbindings.config.istio.io created
customresourcedefinition.apiextensions.k8s.io/quotaspecs.config.istio.io created
customresourcedefinition.apiextensions.k8s.io/rules.config.istio.io created
customresourcedefinition.apiextensions.k8s.io/attributemanifests.config.istio.io created
customresourcedefinition.apiextensions.k8s.io/bypasses.config.istio.io created
customresourcedefinition.apiextensions.k8s.io/circonuses.config.istio.io created
customresourcedefinition.apiextensions.k8s.io/deniers.config.istio.io created
customresourcedefinition.apiextensions.k8s.io/fluentds.config.istio.io created
customresourcedefinition.apiextensions.k8s.io/kubernetesenvs.config.istio.io created
customresourcedefinition.apiextensions.k8s.io/listcheckers.config.istio.io created
customresourcedefinition.apiextensions.k8s.io/memquotas.config.istio.io created
customresourcedefinition.apiextensions.k8s.io/noops.config.istio.io created
customresourcedefinition.apiextensions.k8s.io/opas.config.istio.io created
customresourcedefinition.apiextensions.k8s.io/prometheuses.config.istio.io created
customresourcedefinition.apiextensions.k8s.io/rbacs.config.istio.io created
customresourcedefinition.apiextensions.k8s.io/redisquotas.config.istio.io created
customresourcedefinition.apiextensions.k8s.io/servicecontrols.config.istio.io created
customresourcedefinition.apiextensions.k8s.io/signalfxs.config.istio.io created
customresourcedefinition.apiextensions.k8s.io/solarwindses.config.istio.io created
customresourcedefinition.apiextensions.k8s.io/stackdrivers.config.istio.io created
customresourcedefinition.apiextensions.k8s.io/statsds.config.istio.io created
customresourcedefinition.apiextensions.k8s.io/stdios.config.istio.io created
customresourcedefinition.apiextensions.k8s.io/apikeys.config.istio.io created
customresourcedefinition.apiextensions.k8s.io/authorizations.config.istio.io created
customresourcedefinition.apiextensions.k8s.io/checknothings.config.istio.io created
customresourcedefinition.apiextensions.k8s.io/kuberneteses.config.istio.io created
customresourcedefinition.apiextensions.k8s.io/listentries.config.istio.io created
customresourcedefinition.apiextensions.k8s.io/logentries.config.istio.io created
customresourcedefinition.apiextensions.k8s.io/edges.config.istio.io created
customresourcedefinition.apiextensions.k8s.io/metrics.config.istio.io created
customresourcedefinition.apiextensions.k8s.io/quotas.config.istio.io created
customresourcedefinition.apiextensions.k8s.io/reportnothings.config.istio.io created
customresourcedefinition.apiextensions.k8s.io/servicecontrolreports.config.istio.io created
customresourcedefinition.apiextensions.k8s.io/tracespans.config.istio.io created
customresourcedefinition.apiextensions.k8s.io/rbacconfigs.rbac.istio.io created
customresourcedefinition.apiextensions.k8s.io/serviceroles.rbac.istio.io created
customresourcedefinition.apiextensions.k8s.io/servicerolebindings.rbac.istio.io created
customresourcedefinition.apiextensions.k8s.io/adapters.config.istio.io created
customresourcedefinition.apiextensions.k8s.io/instances.config.istio.io created
customresourcedefinition.apiextensions.k8s.io/templates.config.istio.io created
customresourcedefinition.apiextensions.k8s.io/handlers.config.istio.io created

```

Now let's install Istio with mutual TLS authentication

```
kubectl apply -f install/kubernetes/istio-demo-auth.yaml
```

Verify the installation with 

```
kubectl get svc -n istio-system
```

And the output is 

```
NAME                       TYPE           CLUSTER-IP       EXTERNAL-IP   PORT(S)                                                                                                                   AGE
grafana                    ClusterIP      10.102.40.127    <none>        3000/TCP                                                                                                                  50s
istio-citadel              ClusterIP      10.104.203.79    <none>        8060/TCP,9093/TCP                                                                                                         49s
istio-egressgateway        ClusterIP      10.105.163.172   <none>        80/TCP,443/TCP                                                                                                            50s
istio-galley               ClusterIP      10.96.5.26       <none>        443/TCP,9093/TCP                                                                                                          50s
istio-ingressgateway       LoadBalancer   10.103.22.201    <pending>     80:31380/TCP,443:31390/TCP,31400:31400/TCP,15011:31730/TCP,8060:31818/TCP,853:30230/TCP,15030:30353/TCP,15031:30787/TCP   50s
istio-pilot                ClusterIP      10.109.168.91    <none>        15010/TCP,15011/TCP,8080/TCP,9093/TCP                                                                                     49s
istio-policy               ClusterIP      10.106.71.127    <none>        9091/TCP,15004/TCP,9093/TCP                                                                                               50s
istio-sidecar-injector     ClusterIP      10.105.249.123   <none>        443/TCP                                                                                                                   48s
istio-statsd-prom-bridge   ClusterIP      10.107.111.244   <none>        9102/TCP,9125/UDP                                                                                                         49s
istio-telemetry            ClusterIP      10.99.67.97      <none>        9091/TCP,15004/TCP,9093/TCP,42422/TCP                                                                                     49s
jaeger-agent               ClusterIP      None             <none>        5775/UDP,6831/UDP,6832/UDP                                                                                                43s
jaeger-collector           ClusterIP      10.96.28.41      <none>        14267/TCP,14268/TCP                                                                                                       44s
jaeger-query               ClusterIP      10.98.247.91     <none>        16686/TCP                                                                                                                 44s
prometheus                 ClusterIP      10.105.37.50     <none>        9090/TCP                                                                                                                  49s
servicegraph               ClusterIP      10.101.245.22    <none>        8088/TCP                                                                                                                  48s
tracing                    ClusterIP      10.105.196.68    <none>        80/TCP                                                                                                                    43s
zipkin                     ClusterIP      10.100.78.219    <none>        9411/TCP                                                                                                                  43s

```

Let's see how many namespaces we have after installing Istio.

```
kubectl get namespaces
NAME           STATUS    AGE
default        Active    54d
istio-system   Active    39m
kube-public    Active    54d
kube-system    Active    54d
```

Install the default application bookinfo

```
kubectl apply -f <(istioctl kube-inject -f samples/bookinfo/platform/kube/bookinfo.yaml)
```

check the services and pods

```
steve@sandbox:~/istio-1.0.2$ kubectl get services
NAME          TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)    AGE
details       ClusterIP   10.106.104.133   <none>        9080/TCP   25s
kubernetes    ClusterIP   10.96.0.1        <none>        443/TCP    54d
productpage   ClusterIP   10.111.85.80     <none>        9080/TCP   24s
ratings       ClusterIP   10.109.108.213   <none>        9080/TCP   25s
reviews       ClusterIP   10.105.228.100   <none>        9080/TCP   25s
steve@sandbox:~/istio-1.0.2$ kubectl get pods
NAME                              READY     STATUS            RESTARTS   AGE
details-v1-566d7d9594-2w6c2       0/2       PodInitializing   0          50s
productpage-v1-7447f6675d-r5lrl   0/2       PodInitializing   0          48s
ratings-v1-647b769c86-6tvck       2/2       Running           0          50s
reviews-v1-64f496d7f8-gdcdw       0/2       PodInitializing   0          49s
reviews-v2-67b9d84556-z8q9b       0/2       PodInitializing   0          49s
reviews-v3-678c559f4-gxz5r        2/2       Running           0          49s

```

Install Istio Gateway so that services can be accessed from outside of cluster.

```
kubectl apply -f samples/bookinfo/networking/bookinfo-gateway.yaml
```

```
kubectl get gateway
NAME               AGE
bookinfo-gateway   1m
```

In order to test gateway, let's install the httpbin with sidecar injected. 

```
kubectl apply -f <(istioctl kube-inject -f samples/httpbin/httpbin.yaml)
```

determine the IP and port of gateway. 

```
kubectl get svc istio-ingressgateway -n istio-system
NAME                   TYPE           CLUSTER-IP      EXTERNAL-IP   PORT(S)                                                                                                                   AGE
istio-ingressgateway   LoadBalancer   10.103.22.201   <pending>     80:31380/TCP,443:31390/TCP,31400:31400/TCP,15011:31730/TCP,8060:31818/TCP,853:30230/TCP,15030:30353/TCP,15031:30787/TCP   1h

```

The external ip is pending which means there is no external load balancer installed. 

As we don't have an external load balancer, we are going to find out the ingress IP and ports using a node port. 

```
export INGRESS_PORT=$(kubectl -n istio-system get service istio-ingressgateway -o jsonpath='{.spec.ports[?(@.name=="http2")].nodePort}')
export SECURE_INGRESS_PORT=$(kubectl -n istio-system get service istio-ingressgateway -o jsonpath='{.spec.ports[?(@.name=="https")].nodePort}')
export INGRESS_HOST=$(kubectl get po -l istio=ingressgateway -n istio-system -o 'jsonpath={.items[0].status.hostIP}')
```


Create an Istio Gateway.

```
cat <<EOF | kubectl apply -f -
apiVersion: networking.istio.io/v1alpha3
kind: Gateway
metadata:
  name: httpbin-gateway
spec:
  selector:
    istio: ingressgateway # use Istio default gateway implementation
  servers:
  - port:
      number: 80
      name: http
      protocol: HTTP
    hosts:
    - "httpbin.example.com"
EOF
```

Create a virtual service

```
cat <<EOF | kubectl apply -f -
apiVersion: networking.istio.io/v1alpha3
kind: VirtualService
metadata:
  name: httpbin
spec:
  hosts:
  - "httpbin.example.com"
  gateways:
  - httpbin-gateway
  http:
  - match:
    - uri:
        prefix: /status
    - uri:
        prefix: /delay
    route:
    - destination:
        port:
          number: 8000
        host: httpbin
EOF
```

Access the service from curl.

```
curl -I -HHost:httpbin.example.com http://$INGRESS_HOST:$INGRESS_PORT/status/200
```

The result should be something like this.

```
HTTP/1.1 200 OK
server: envoy
date: Sun, 23 Sep 2018 15:10:15 GMT
content-type: text/html; charset=utf-8
access-control-allow-origin: *
access-control-allow-credentials: true
content-length: 0
x-envoy-upstream-service-time: 9

```

Now, let's create a GATEWAY_URL

```
export GATEWAY_URL=$INGRESS_HOST:$INGRESS_PORT
```

To confirm that the Bookinfo application is running

```
curl -o /dev/null -s -w "%{http_code}\n" http://${GATEWAY_URL}/productpage
```

You can also access the productpage content with the following curl command.

```
curl http://$GATEWAY_URL/productpage
```

Now let's do a performance test for the productpage. 

```
wrk -t4 -c128 -d30s http://$GATEWAY_URL -s pipeline.lua --latency -- /productpage 16
Running 30s test @ http://38.113.162.53:31380
  4 threads and 128 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency     0.00us    0.00us   0.00us    -nan%
    Req/Sec    11.25      9.82    40.00     73.42%
  Latency Distribution
     50%    0.00us
     75%    0.00us
     90%    0.00us
     99%    0.00us
  128 requests in 30.09s, 680.25KB read
Requests/sec:      4.25
Transfer/sec:     22.61KB

```

It is a little bit surprise that the application is very slow with microservice as backend. It is expected to be slow but 4 request per second is not expected. It looks like we have put too much load on it. Let's remove the pipeline and use only one thread with 100 connections. 

```
wrk -t1 -c100 -d30s http://$GATEWAY_URL/productpage
Running 30s test @ http://38.113.162.53:31380/productpage
  1 threads and 100 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency   114.15ms  324.20ms   1.94s    92.24%
    Req/Sec    30.28     20.47   140.00     76.92%
  839 requests in 30.04s, 3.30MB read
  Socket errors: connect 0, read 0, write 0, timeout 607
  Non-2xx or 3xx responses: 213
Requests/sec:     27.93
Transfer/sec:    112.53KB

```

Now it is getting better but we got 213 errors. It looks like the load is still too high.

```
wrk -t1 -c10 -d30s http://$GATEWAY_URL/productpage
Running 30s test @ http://38.113.162.53:31380/productpage
  1 threads and 10 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency   328.26ms  197.74ms 878.17ms   63.76%
    Req/Sec    31.37     17.81   100.00     62.99%
  911 requests in 30.02s, 3.58MB read
  Non-2xx or 3xx responses: 233
Requests/sec:     30.35
Transfer/sec:    122.03KB

```

It is getting a little bit better but with more errors. 

```
wrk -t1 -c1 -d30s http://$GATEWAY_URL/productpage
Running 30s test @ http://38.113.162.53:31380/productpage
  1 threads and 1 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency    78.92ms   17.56ms 173.34ms   71.99%
    Req/Sec    12.67      4.55    20.00     71.33%
  380 requests in 30.04s, 1.98MB read
Requests/sec:     12.65
Transfer/sec:     67.40KB
```

In my cluster, I have three worker nodes and each have 32GB memory and 4vcpus. I am planning to get light-4j chain pattern apia, apib, apic and apid installed and test it so that we can have an apple to apple comparison. 


