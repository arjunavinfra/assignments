Master Assignment 
 
 Run Node Exporter on local machine: https://prometheus.io/docs/guides/node-exporter/
 
 Run Prometheus on local machine: https://prometheus.io/docs/prometheus/latest/getting_started/
 
 Download and run Thanos Sidecar, configure it to read TSDB from local prometheus without bucket config.( Refer https://thanos.io/tip/thanos/quick-tutorial.md/#store-api)
 
  Download and run Thanos Querier, configure it to add the Thanos Sidecar as a store.( Refer https://thanos.io/tip/thanos/quick-tutorial.md/#querierquery)

  Run Grafana on local machine.(Refer https://grafana.com/grafana/download and https://grafana.com/docs/grafana/latest/setup-grafana/installation/debian/#2-start-the-server)
 
 Add Querier as a Datasource in the Grafana and name it as Thanos.
 
 Create a custom dashboard in Grafana and add panels for the following:-
 
[] Disk Usage.(Refer https://devconnected.com/monitoring-disk-i-o-on-linux-with-the-node-exporter/)
[] CPU Usage.(Refer https://www.robustperception.io/understanding-machine-cpu-usage/)
[] Network Usage.(Refer https://www.robustperception.io/network-interface-metrics-from-the-node-exporter/)


#To setup the full stack run the below 


Pre request Install MelalLB from https://kind.sigs.k8s.io/docs/user/loadbalancer/

```ruby
kubectl apply -k ./ 
````

````ruby

List of objects created

arjun@ARJUN-AV:~/Documents/assignments$ kubectl get sts,deploy
NAME                                         READY   AGE
statefulset.apps/prometheus-k8s              1/1     9m17s
statefulset.apps/thanos-ruler-thanos-ruler   1/1     9m17s
statefulset.apps/thanos-store                1/1     11m

NAME                                  READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/grafana               1/1     1            1           11m
deployment.apps/prometheus-operator   1/1     1            1           11m
deployment.apps/thanos-query          1/1     1            1           11m
arjun@ARJUN-AV:~/Documents/assignments$ kubectl get pods
NAME                                   READY   STATUS    RESTARTS   AGE
grafana-9f58f8675-4jbmq                1/1     Running   0          11m
node-exporter-lsl4g                    2/2     Running   0          11m
prometheus-k8s-0                       3/3     Running   0          4m9s
prometheus-operator-5cd6dbfd4f-gs5dh   2/2     Running   0          11m
thanos-query-76d6f4dfc-7t45s           1/1     Running   0          11m
thanos-ruler-thanos-ruler-0            2/2     Running   0          9m36s
thanos-store-0                         1/1     Running   0          11m
arjun@ARJUN-AV:~/Documents/assignments$ kubectl get svc 
NAME                    TYPE           CLUSTER-IP      EXTERNAL-IP      PORT(S)               AGE
grafana                 ClusterIP      10.96.147.146   <none>           3000/TCP              11m
grafana-external        LoadBalancer   10.96.133.193   172.18.255.200   3000:30639/TCP        11m
node-exporter           ClusterIP      None            <none>           9100/TCP              11m
prometheus-external     LoadBalancer   10.96.127.120   172.18.255.201   9090:30158/TCP        11m
prometheus-k8s          ClusterIP      10.96.137.150   <none>           9090/TCP,8080/TCP     11m
prometheus-operated     ClusterIP      None            <none>           9090/TCP,10901/TCP    9m43s
prometheus-operator     ClusterIP      None            <none>           8443/TCP              11m
thanos-query            ClusterIP      10.96.115.124   <none>           10902/TCP             11m
thanos-query-external   LoadBalancer   10.96.27.48     172.18.255.202   10902:32503/TCP       11m
thanos-ruler            ClusterIP      10.96.229.76    <none>           10901/TCP,10902/TCP   11m
thanos-ruler-operated   ClusterIP      None            <none>           10902/TCP,10901/TCP   9m43s
thanos-sidecar          ClusterIP      None            <none>           10901/TCP             11m
thanos-store            ClusterIP      None            <none>           10901/TCP,10902/TCP   11m
arjun@ARJUN-AV:~/Documents/assignments$ 

```

login to prometheus UI , Thanos UI ,Grafana UI with the loadBalancer IP Address 


Grafana Username and Password is `admin`



