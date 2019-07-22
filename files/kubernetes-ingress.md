<h1 class="title" style="display:none">Kubernetes ingress</h1>


```groovy
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: my-cip-ingress
  annotations:
    kubernetes.io/ingress.global-static-ip-name: "web-static-ip"
spec:
  backend:
    serviceName: my-cip-service
    servicePort: 8080

```