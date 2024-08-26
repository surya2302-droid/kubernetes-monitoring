# INSTALLATION STEPS FOR K8s Dashboard

` kubectl apply -f dashboard-setup.yaml`

this will install all the requireds services for kubernetes dashboard. to enable ingress use the below steps if have configured traefik and cert manager otherwise use any preferred ingress like istio or nginx

to get the certificate 
`kubectl apply -f k8s-dashboard-cert.yaml`

to install ingress route

`kubectl apply -f ingress.yaml`