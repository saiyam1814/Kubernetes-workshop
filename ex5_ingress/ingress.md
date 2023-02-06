## Make sure to have an ingress controller installed on your Kubernetes cluster, once you have that installed, you need to create the below ingress yaml file and change the host accordingly.


```
version=$(curl -s "https://api.github.com/repos/kubernetes/ingress-nginx/releases" | grep tag_name | grep controller | sort -r | awk -F'"' 'NR==1 {print $4}')

kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/${version}/deploy/static/provider/cloud/deploy.yaml
```

```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  annotations:
    cert-manager.io/cluster-issuer: letsencrypt-prod
    kubernetes.io/ingress.class: traefik
  name: kubeworkshop-ingress
  namespace: demo
spec:
  rules:
  - host: navigate.youclusterID
    http:
      paths:
      - backend:
          service:
            name: kubeworkshop
            port:
              number: 80
        path: /
        pathType: Prefix
  tls:
  - hosts:
    - demo.youclusterID
    secretName: demo

```
