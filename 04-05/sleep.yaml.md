```yaml
mkdir -p /opt/k8s/work/istio_first/sleep/
cat <<EOF > /opt/k8s/work/istio_first/sleep/sleep.yaml
apiVersion: v1
kind: Service
metadata:
  name: sleep
  labels:
    app: sleep
    version: v1
spec:
  selector:
    app: sleep
    version: v1
  ports:
    - name: ssh
      port: 80
---
apiVersion: extensions/v1beta1
kind: Deployment
metadata:
  name: sleep
spec:
  replicas: 1
  template:
    metadata:
      labels:
        app: sleep
        version: v1
    spec:
      containers:
      - name: sleep
        image: dustise/sleep
        imagePullPolicy: IfNotPresent
EOF
```


