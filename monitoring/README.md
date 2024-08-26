# before installation:- 

run on a linux machine

```
echo -n 'adminuser' > ./admin-user # change your username
echo -n 'p@ssword!' > ./admin-password # change your password
```


` kubectl create secret generic grafana-admin-credentials --from-file=./admin-user --from-file=admin-password -n monitoring `
now to install 

# HELM COMMAND TO INSTALL GRAFANA AND PROMETHEUS
```
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
helm install -n monitoring prometheus prometheus-community/kube-prometheus-stack -f grafana.yaml
```


# HELM COMMAND TO INSTALL LOKI AND PROMTAIL



```
helm repo add grafana https://grafana.github.io/helm-charts
helm repo update

helm upgrade --install loki grafana/loki-distributed -n monitoring
helm upgrade --install promtail grafana/promtail --values promtail-config.yaml -n monitoring
```


# ADD INGRESS GATEWAY TO GRAFANA WITH TRAEFIK INGRESS (Optional)  

### this part only works with traefik and certmanager configured. otherwise use any preferred ingress like istio or nginx 

make sure you already have traefik installed and configured and have proper dns records set 

to get a certificate from letsencrypt using certmanager

`kubectl apply -f grafana-cert.yaml`

to install ingress route

`kubectl apply -f ingress.yaml`