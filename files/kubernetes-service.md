<h1 class="title" style="display:none">Kubernetes service</h1>


```groovy
apiVersion: v1
kind: Service
metadata:
  name: my-cip-service
spec:
  type: ClusterIP
  selector:
    app: metrics
    department: sales
  ports:



protocol: TCP
port: 80
targetPort: 8080

```